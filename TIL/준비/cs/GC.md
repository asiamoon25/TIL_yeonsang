GC 들어가기 전에 JVM 에서 메모리를 어떻게 보는지 확인해보자.
# JVM이 보는 메모리...


## JVM 메모리 영역

_일반적으로 애플리케이션에서 사용되는 객체는 오래 유지되는 객체보다 잠시 사용되는 경우가 많음._
![[Pasted image 20240401181520.png]]
* Young Generation : 새롭게 생성하는 객체들이 존재하는 곳
* Old Generation : Young Generation 영역에서 오랫동안 살아남은 객체(가중치) 들이 존재하는 곳
* Meta Space : 클래스의 메타데이터, 문자열 정보를 저장하는 영역(JAVA 8 부터)
* YG 와 OG 로 나눈 이유는 애플리케이션에서의 객체의 수명은 대부분 짧기 때문에 효율적으로 관리하기 위함.

## JVM 이 메모리를 관리하는 방식
### Heap 메모리의 구조

Heap 영역은 처음 설계될 때 다음의 2가지를 전제로 설계 되었음.
1. 대부분의 객체는 금방 접근 불가능한 상태가 된다.(Unreachable)
2. 오래된 객체에서 새로운 객체로의 참조는 아주 적게 존재한다.

➡️ 객체는 대부분 일회성이며, 메모리에 오래 남아있는 경우는 드물다.

* **대부분의 객체는 금방 접근 불가능한 상태가 된다.**
![[Pasted image 20240402113722.png]]
	해당 이미지를 보면 알 수 있듯이 Young Generation 에서 Old Generation 으로 가는 객체들은 별로 없는것을 알 수 있다.
	이는 대부분의 객체는 금방 접근 불가능한 상태가 된다 라는 말과 같다.


* **오래된 객체에서 새로운 객체로의 참조가 적다**
	위 전제는 GC가 효율적으로 메모리를 관리할 수 있도록 도와줌.
	
	오래된 객체가 새로운 객체로의 참조를 거의 가지지 않는다고 하면, Young Generation 에서 발생하는 대부분의 GC 는 Old Generation 의 객체들을 검사할 필요가 없다는 것을 의미한다. 이로 인해 GC 성능이 크게 향상됨.

이로 인해 Young Generation 과 Old Generation 으로 구분 된듯 하다.

### 구현과 최적화
* Write Barrier : 위 가설을 실제 시스템에서 구현하기 위해, JVM 은 Write Barrier 를 사용하여 Old Generation의 객체가 Young Generation의 객체를 참조할 때 이를 추적함. 이는 Old Generation 에서 Young Generation 으로의 참조가 생성될 때마다 특정 조치를 취할 수 있게 해주며, 전체 Heap 을 스캔할 필요 없이 효율적으로 GC 를 수행할 수 있음.
  
* Card Marking
	* Card Table : Old Generation 내 각 부분을 추적하기 위한 바이트 배열.
	  각 원소는 Old Generation 의 512byte 크기 구역을 나타낸다. Card Table 은 Old Generation의 메모리를 작은 블록(카드) 로 나누고, 각 블록이 어떤 상태인지를 기록하는 지도 같은 역할
	  Card Table 은 OG 를 512 바이트로 쪼갠 것 중 하나가 Card 임.
	  
	* Card Marking : Old Generation 의 객체가 YG 의 객체를 참조할 때, 해당 참조 정보를 카드 테이블에 기록함. 객체의 참조형 필드값이 변경되면, 해당 객체가 위치한 메모리 구역(카드)을 "Dirty(더러워졌다)"라고 표시함.
	  
	* 카드 마킹 과정
		1. 참조 생성 : OG 의 객체가 YG의 객체를 처음 참조하게 되면, 이 관계는 카드 테이블에 "더러워짐" 으로 표시됨.
		2. GC 시 : YG 에서 GC가 실행될 때, 전체 OG 를 검사할 필요 없이 "더러워진" 카드만 확인하면 됨. 이를 통해서 OG 객체가 YG 객체를 참조하고 있는지 빠르게 파악 가능
		3. 효율적인 GC : 이 방식 덕분에, YG의 GC 속도가 크게 향상됨. 전체 OG 를 검사하는 대신, 변경된 참조만 확인함.
	* 세부사항
		* 카드 테이블 구현 : 카드 테이블의 각 항목은 OG의 512 바이트 영역을 나타냄. 객체의 참조형 필드가 변경될 때, 해당 객체가 속한 영역(카드)의 인덱스는 객체의 메모리 주소를 512(2^9)로 나눈 값에 해당함.
		  이는 객체 주소를 오른쪽으로 9비트 시프트함으로써 계산됨.
		* 더러움 표시 : 카드가 "더러워 졌다"고 표시되는 것은, 해당 영역에 있는 OG 객체가 YG 객체를 참조하고 있다는 뜻임. 이 표시를 통해 GC는 해당 영역만 검사하여 참조를 빠르게 파악할 수 있음.

**아니 그러면 512바이트 영역을 벗어나서 카드 2개에 걸쳐서 있으면 어캄?**
➡️ 일단 JAVA 의 객체가 512byte 를 넘어가는 경우는 거의 없음.
그리고 객체의 참조가 변경되어 카드 테이블에 "더러워진" 표시를 해야 할 때, 실제 메모리 위치와는 무관하게 처리됨. 객체가 512byte 경계를 넘어서는 경우에도, 해당 객체의 시작 주소가 속한 카드만이 "더러워진" 상태로 마킹됨. 결국은 객체의 시작 주소만 조짐.

다음 부분에서 부터 GC 시작

---
# GC (Garbage Collector)

## GC 란?

Garbage Collector

* 자바 애플리케이션에서 사용하지 않는 메모리를 자동으로 수거하는 기능
* Heap 영역 에서 동적으로 할당했던 메모리 중 필요 없게 된 메모리 객체(garbage) 를 모아 주기적으로 제거 하는 프로세스를 말함.


## GC 왜 중요함?

1. 메모리 누수 방지
	프로그램이 더 이상 사용하지 않는 메모리를 계속 점유하는 현상을 말한다. 이는 특히 장시간 실행되는 애플리케이션에서 심각한 성능 저하와 시스템 불안정을 초래할 수 있음. GC 는 이러한 누수들을 효과적으로 방지함.

2. 프로그래머의 편의성 향상
	자동 메모리 관리를 통해, 프로그래머는 메모리 할당과 해제에 대해 걱정할 필요가 없어졌음.

3. 애플리케이션 성능 향상
	적절하게 구성된 GC 는 애플리케이션의 성능을 향상 시킬 수 있음.
	GC 는 메모리를 재활용하여, 새 객체 할당 시 발생할 수 있는 메모리 할당 지연을 줄여줌. 또한, 최신 GC 는 멀티코어 프로세서를 활용하여 병렬로 GC를 수행함으로써 성능을 최적화 함.

4. 애플리케이션 안정성 증가
	메모리를 수동으로 관리할 때 발생할 수 있는 다양한 오류(예: 잘못된 메모리 접근, 이중 해제 등)를 방지함으로써, 애플리케이션이 보다 안정적으로 실행될 수 있게 도와준다.

5. 프로그래밍 모델 단순화
	메모리 관리 로직을 프로그램 코드에서 분리함으로써, 코드가 더 간결하고 읽기 쉬워짐.


## GC 대상
_죽창의 대상 Garbage..._
![[Pasted image 20240401184813.png]]
_GC 알긴 아는데 어떻게 할당된 메모리 회수함?_

GC 는 특정 객체가 garbage 인지 아닌지 판단하기 위해서 도달성, 도달 능력(Reachability) 라는 개념을 적용함.

객체에 레퍼런스가 있다면 Reachable 로 구분되고, 객체에 유효한 레퍼런스가 없다면 Unreachable 로 구분하고 수거한다.

* Reachable : 객체가 참조되고 있는 상태
* Unreachable : 객체가 참조되고 잇지 않은 상태(GC 의 대상)

_그래서 어떻게?_
![[Pasted image 20240401185745.png]]
#### Mark-Sweep
* GC 대상이 될 대상 객체를 식별(Mark) 하고 제거(Sweep) 하며 객체가 제거되어 파편화된 메모리 영역을 앞에서부터 채워나가는 작업(Compaction) 을 수행함.
  
* Mark : 먼저 Root Space 로 부터 그래프 순회를 통해 연결된 객체들을 찾아내어 각각 어떤 객체를 참조하고 있는지 찾아서 마킹
  
* Sweep : 참조하고 있지 않은 객체 즉 Unreachable 객체들을 Heap 에서 제거
  
* Compact : Sweep 후에 분산된 객체들을 Heap 의 시작 주소로 모아 메모리가 할당된 부분과 그렇지 않은 부분으로 압축함.(GC 종류에 따라 하지 않는 경우도 있음.) 
⬇️ 아래에 자세하게 써놓음

1. Root 집합 탐색 : GC 과정은 루트집합(Root Set) 으로 부터 시작함. 루트 집합에는 애플리케이션에서 직접적으로 접근할 수 있는 객체들의 참조가 포함되어 있으며, 이는 스택의 지역 변수, 정적 변수 등으로부터의 참조를 포함
   
2. 참조된 객체 탐색 : 루트 집합에서 접근할 수 있는 객체들을 시작점으로 하여, 이 객체들이 참조하는 다른 객체들을 재귀적으로 탐색함. 이 과정에서 접근 가능한 모든 객체가 식별됨.
   
3. 가비지 식별 : 이 탐색 과정을 통해 도달할 수 없는 객체, 즉 루트 집합에서 어떤 경로를 통해서도 참조 될 수 없는 객체들이 가비지로 식별된다. 이러한 객체들은 더 이상 사용되지 않으므로 메모리를 점유할 필요가 없어짐.
   
4. 메모리 회수 : 식별된 가비지 객체들의 메모리는 GC에 의해 회수됨. 회수된 메모리 공간은 새로운 객체를 위해 재사용 될 수 있음.


### Minor GC
![[Pasted image 20240401182215.png]]

New/Young 영역을 Minor GC 라고 부름. New/Young 영역은 다시 Eden / Survivor 라는 영역으로 나뉨.

* Eden
	* 자바 객체가 생성되자마자 저장되는 곳.
	* GC 후 살아남은 객체들은 Survivor 영역으로 보냄.
* Survivor
	* 해당 영역은 다시 survivor1, survivor2 로 나뉨.
	* 최소 1번의 GC 이상 살아남은 객체가 존재하는 영역

**Minor GC 발생 시**
처음 생성된 객체는 YG 영역의 일부인 Eden 영역에 위치한다.
1. Eden 영역 꽉참 ➡️ Minor GC 실행
2. Mark 동작을 통해 reachable 객체를 탐색
3. Eden 영역에서 살아남은 객체는 1개의 Survivor 영역으로 이동
4. Eden 영역에서 사용되지 않는 객체(unreachable) 의 메모리 해제(sweep)
5. 살아남은 모든 객체들은 age 값이 1씩 증가
6. 다시 GC 발생 시 전 GC에서 survivor1 이 사용되었으면 survivor2 를 사용해서 survivor2 로 활성 객체들을 다 넘김

> **age?**
> Survivor 영역에서 객체가 살아남은 횟수를 의미, Object Header 에 기록됨.
> age 갑이 임계값에 다다르면 Promotion(OG 영역으로 이동) 여부를 결정
> JVM 중 가장 일반적인 HotSpot JVM 의 경우 이 age의 기본 임계 값은 31이다.
> 객체 헤더에 age를 기록하는 부분이 6bit로 되어 있기 때문
> 
> 또한 Survivor 영역의 제한 조건으로 Survivor 영역 중 반드시 1개는 사용되어야 하고, 나머지는 비어 있어야 한다.   
  만약 두 Survivor 영역에 모두 데이터가 존재하거나, 모두 사용량이 0이라면 현재 시스템이 정상적인 상황이 아니라는 반증이 된다.


이러한 방식은 속도가 매우 빠르며 작은 크기의 메모리를 콜렉팅하는데 매우 효과적이다.
Minor GC 의 경우에는 자주 일어나기 때문에 GC에 걸리는 시간이 짧은 알고리즘들이 적합함.

### Major GC (Old Generation GC, Full GC)
![[Pasted image 20240401182215.png]]

* OG는 길게 살아남는 메모리들이 존재하는 공간
* OG 의 객체들은 처음에는 YG에서 시작되었으나, GC 과정 중에 제거되지 않은 경우 age 임계값이 차게되어 이동된 녀석들
* Major GC 는 객체들이 계속 Promotion 되어 Old Generation 영역이 가득 차면 발생
* 느림
* OG 는 넓고 GC 를 돌리면 JAVA application 을 잠시 멈추기 때문에 STOP-THE-WORLD 가 일어난다.
![[Pasted image 20240401181931.png]]
* Stop The World
	GC 를 위해 어플리케이션을 일시적으로 멈추는 것

다음 부분에서 Stop The World 방어전을 위한 Java 개발자들의 노력이 나옴

---
## GC 알고리즘 종류

_설정을 통해서 JAVA 에 적용가능한거 앎?_

### Serial GC

* YG 영역은 위에 나온 Mark and Sweep 알고리즘대로 수행되지만 OG 에서는 Mark Sweep Compact 알고리즘이 사용되는데, 기존 Mark and Sweep 에 Compact 라는 작업이 추가됨.
* Compact
	* heap 영역을 정리하기 위한 단계로 유효한 객체들이 연속되게 쌓이도록 Heap 의 가장 앞 부분부터 채워서 객체가 존재하는 부분과 객체가 존재하지 않는 부분으로 나누는 것

* 옵션 넣는 방법
```shell
java -XX:+UseSerialGC -jar Application.java
```

<span style="color:red">주의 사항</span>
* Serial GC 는 서버의 CPU 코어가 1개일 때 사용하기 위해 개발되었으며, 모든 GC 일을 처리하기 위해 1개의 쓰레드만을 사용한다. 그렇게 때문에 CPU 코어가 여러개인 운영서버에서 Serial GC 를 사용하는 것은 피해야한다.
### Parallel GC
* Throughput GC 로도 알려져있음.
* 기본 과정은 Serial GC 와 동일
* 차이점은 여러 개의 쓰레드를 통해 Parallel 하게 GC 를 수행
* 옵션
```shell
java -XX:+UserParallelGC -jar Application.jar

//사용할 스레드 갯수
-XX:ParallelGCThreads=<num>

//최대 지연 시간
-XX:MaxGCPauseMillis=<num>
```

* GC의 오버헤드를 상당히 줄여주었고,JAVA 8 까지 기본 GC 로 사용되었음. 그럼에도 불구하고 Application 이 멈추는 것은 피할 수 없었다.


#### Parallel Old GC (Parallel Compacting Collector)

* JDK5 update6 부터 제공한 GC
* Parallel GC 와 Old 영역의 GC 알고리즘만 다름.
* Mark Sweep Compact 가 아닌 Mark Summary Compaction 이 사용됨.
  Summary 단계에서는 앞서 GC를 수행한 영역에 대해서 별도로 살아있는 객체를 색별한다는 점에서 다르고 조금 더 복잡함.

#### CMS GC(Concurrent Mark Sweep)
* Parallel GC 와 마찬가지로 여러 개의 쓰레드를 이용함.
* 기존 Serial GC 나 Parallel GC 와 다르게 Mark Sweep 알고리즘을 Concurrent 하게 수행함.
![[Pasted image 20240402145636.png]]
* CMS GC는 애플리케이션의 지연 시간을 최소화 하기 위해 고안되었으며, 애플리케이션이 구동중일 때 프로세서의 자원을 공유하여 이용가능해야 한다. CMS GC가 수행될 때에는 자원이 GC를 위해서도 사용되므로 응답이 느려질 순 있지만 응답이 멈추지는 않게 된다.
* 옵션
```shell
java -XX:+UseConcMarkSweepGC -jar Application.java
```

<span style="color:red">주의점</span>
이러한 GC 는 다른 GC 방식 보다 메모리와 CPU 를 더 많이 필요로 하며, Compaction 단계를 수행하지 않는다는 단점이 있음.
장기적으로 운영되면 조각난 메모리들이 많아 Compaction 단계가 수행되면 오히려 Stop The World 시간이 길어지는 문제가 발생함.

### G1 GC(Garbage First GC)

* JAVA 7 부터 지원되기 시작
* 기존 GC 알고리즘에서는 Heap 영역을 물리적으로 Young 영역 과 Old 영역으로 나누어 사용했음. 
  G1 GC 는 Eden 영역에 할당하고, Survivor로 카피하는 등의 과정을 사용하지만 물리적으로 메모리 공간을 나누지는 않음.
  대신 Region(지역) 이라는 개념을 새로 도입하여 Heap 을 균등하게 여러 개의 지역으로 나누고, 각 지역을 역할과 함께 논리적으로 구분하여 (Eden 인지, Survivor 인지, Old 인지) 객체를 할당함.
* 옵션
```shell
java -XX:+UseG1GC -jar Application.java
```

![[Pasted image 20240402150720.png]]

G1 GC에서는 Eden, Survivor, Old 역할에 더해 Humonogous와 Availabe/Unused라는 2가지 역할을 추가하였다. 

Humonguous는 Region 크기의 50%를 초과하는 객체를 저장하는 Region을 의미하며, Availabe/Unused는 사용되지 않은 Region을 의미한다. 

G1 GC의 핵심은 Heap을 동일한 크기의 Region으로 나누고, 가비지가 많은 Region에 대해 우선적으로 GC를 수행하는 것이다. 

그리고 G1 GC도 다른 가비지 컬렉션과 마찬가지로 2가지 GC(Minor GC, Major GC)로 나누어 수행됨.

#### Minor GC
한 지역에 객체를 할당하다가 해당 지역이 꽉 차면 다른 지역에 객체를 할당하고, Minor GC가 실행된다. 
G1 GC는 각 지역을 추적하고 있기 때문에, 가비지가 가장 많은(Garbage First) 지역을 찾아서 Mark and Sweep를 수행한다.

Eden 지역에서 GC가 수행되면 살아남은 객체를 식별(Mark)하고, 메모리를 회수(Sweep)한다. 
그리고 살아남은 객체를 다른 지역으로 이동시키게 된다. 
복제되는 지역이 Available/Unused 지역이면 해당 지역은 이제 Survivor 영역이 되고, Eden 영역은 Available/Unused 지역이 된다.

#### Major GC
시스템이 계속 운영되다가 객체가 너무 많아 빠르게 메모리를 회수 할 수 없을 때 Major GC(Full GC)가 실행된다. 
그리고 여기서 G1 GC와 다른 GC의 차이점이 두각을 보인다.

기존의 다른 GC 알고리즘은 모든 Heap의 영역에서 GC가 수행되었으며, 그에 따라 처리 시간이 상당히 오래 걸렸다. 
하지만 G1 GC는 어느 영역에 가비지가 많은지를 알고 있기 때문에 GC를 수행할 지역을 조합하여 해당 지역에 대해서만 GC를 수행한다. 
그리고 이러한 작업은 Concurrent하게 수행되기 때문에 애플리케이션의 지연도 최소화할 수 있는 것이다.



### Shenandoah GC

* JDK 8, 11, 12
* G1 GC 를 기반으로 만들어짐.
* 큰 GC 작업을 적은 횟수로 수행하는 것보다 작은 GC를 여러번 수행하는게 더 좋다는 개념을 적용해 만들어진 GC
* Concurrency 를 보장
* GC 가 CPU를 더 사용하는 대신 Pause 시간을 줄이겠다는 의미
* 옵션
```shell
java -XX:+UseShenandoahGC -Xlog:gc -version
```
#### 동작과정
![[Pasted image 20240402151218.png]]
1. Initial Marking
2. Concurrent Marking
3. Final Marking
4. Concurrernt Compaction
Pause 후 root set 을 스캔하고 Java 쓰레드와 동시에 Marking 을 수행.
그 이후 한번 더 pause 를 수행하여 final marking 을 수행하고 압축 마지막 단계에서 marking 된 객체들을 제거.
전체 흐름은 CMS GC 와 비슷.

### ZGC(Z Garbage Collector)
* jdk 11 이상만 지원



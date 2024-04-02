---
sticker: emoji//1f3b0
---
_가상 머신인줄로만 알았다..._
# JVM 이란?

* Java Virtual Machine 의 줄임말
* OS 에 종속 받지 않고 CPU가 Java 를 인식, 실행할 수 있게 하는 가상 컴퓨터
* 또한 가장 중요한 메모리 관리, Garbage Collection 을 수행한다.

### 특징

1. 컴파일된 bytecode 를 기계가 이해할 수 잇는 기계어로 변환
2. 스택 기반의 가상머신 => 연산을 실행할 때, 데이터를 임시로 저장하기 위해 스택 자료구조를 활용한다는 의미
3. 메모리 관리와 GC 를 수행

---


### JVM 구조와 작동원리
![[Pasted image 20240401142940.png]]

JVM 구조에는 크게 Class Loader, Runtime Data Area, Execution Engine, GC 로 나누어져 있다.

**Class Loader** : 클래스 파일을 Runtime Data Area의 메서드 영역으로 불러오는 역할을 한다.

**Execution Engine** : .class 와 같은 bytecode 를 실행 가능하도록 해석한다.

**Runtime Data Area** : 런타임 시 클래스 데이터와 같은 메타 데이터와 실제 데이터가 저장되는 곳이다. Runtime Data Area 는 Method Area, Heap, PC Registers, Java Stacks, Native Method Stacks 로 나누어진다.



#### Class Loader

* Loading
	* 자바 바이트 코드(.class)를 메소드 영역에 저장한다.
	* 각 자바 bytecode 는 JVM 에 의해 메소드 영역에서 다음 정보들을 저장한다.
		* 로드된 클래스를 비롯한 그의 부모 클래스의 정보
		* 클래스 파일과 Class, Interface, Enum 의 관련 여부
		* 변수나 메소드 등의 정보
* Linking
	* Verifying(검증)
		* 읽어 들인 클래스가 자바 언어 명세 및 JVM 명세에 명시된 대로 잘 구성되어 있는지 검사함.
	* Preparing(준비)
		* 클래스가 필요로 하는 메모리를 할당하고, 클래스에서 정의된 필드, 메소드, 인터페이스를 나타내는 데이터 구조를 준비한다.
	* Resolving(분석)
		* 심볼릭 메모리 레퍼런스를 메소드 영역에 있는 실제 레퍼런스로 교체함.
* Initialization
	* 클래스 변수들을 적절한 값으로 초기화 함. 즉, static 필드들이 설정된 값으로 초기화함.

**Class Loader 종류**
![[Pasted image 20240401150810.png]]


1. BootStrap Class Loader(부트스트랩 클래스 로더)
	* JVM 시작 시 가장 최초로 실행되는 클래스로더
	* 자바 클래스를 로드하는 것이 아닌, 자바 클래스를 로드할 수 있는 자바 자체의 클래스 로더와 최소한의 자바 클래스(java.lang.Object, Class, ClassLoader) 만을 로드함.
	  
	  **JAVA8**
	  jre/lib/rt.jar 및 기타 핵심 라이브러리와 같은 JDK의 내부 클래스를 로드함.
	  
	  **JAVA9 이후**
	  더 이상 /re.jar 는 존재하지 않으며, /lib 내에 모듈화되어 포함됬음.
	  이제는 정확하게 ClassLoader 내 최상위 클래스들만 로드함.

2. Extension Class Loader(확장 클래스 로더)
	* BootStrap Class Loader 를 부모로 갖는 클래스 로더
	* 확장 자바 클래스들을 로드한다. java.ext.dirs 환경 변수에 설정된 디렉토리의 클래스 파일을 로드하고, 이 값이 설정되어 있지 않은 경우 ${JAVA_HOME}/jre/lib/ext 에 있는 클래스 파일을 로드함.

3. System Class Loader(시스템 클래스 로더)
	* 자바 프로그램 실행 시 지정한 Classpath 에 있는 클래스 파일 혹은 jar에 속한 클래스들을 로드한다. ➡️ 우리가 만든 .class 확장자 파일 로드


**Class Loader 동작 방식**

Class Loader 는 새로운 Class 를 로드해야할 때, 다음과 같은 방식으로 로드를 수행함.

1. JVM 의 메소드 영역에 클래스가 로드되어 있는지 확인한다. 로드되어 있는 경우 해당 클래스를 사용
2. 메소드 영역에 클래스가 로드되어 있지 않은 경우, System Class Loader 에 Class Load 를 요청한다.
3. System Class Loader 는 Extension Class Loader에게 요청을 넘김
4. Extension Class Loader는 확장 Classpath(JDK/JRE/LIB/EXT) 에 해당 클래스가 있는지 확인 후 존재하지 않으면 System Class Loader에게 요청을 넘김
5. System Class Loader는 시스템 Classpath 에 해당 클래스가 있는지 확인. 클래스가 존재하지 않는 경우 ClassNotFoundException 을 발생.



**Class Loader가 지켜야할 3가지 원칙**
* 위임 원칙
	* 클래스 로더는 클래스 또는 리소스를 찾기 위해 요청을 받았을 때, 상위 클래스 로더에게 책임을 위임하는 위임 모델을 따른다.
* 가시 범위 원칙
	* 하위 클래스 로더는 상위 클래스 로더가 로드한 클래스를 볼 수 있지만, 반대로 상위 클래스 로더는 하위 클래스 로더가 로드한 클래스를 알 수 없다.
		* 1. 보안 : Bootstrap Class Loader 가 하위 클래스로더에서 로드한 클래스를 볼 수있으면 악의적으로 저작된 클래스를 참조할 수 있다면,전체 시스템의 보안에 심각한 위협이 될 수 있음.
		* 2. 모듈성 : 다른 소스로부터 동일한 이름을 가진 클래스가 로드될 수 있으며, 이는 서로 다른 모듈이나 애플리케이션이 서로 충돌 없이 공존할 수 있도록 한다.
		* 3. 네임스페이스 관리 : 패키지의 물리적인 구조와는 독립적으로, 런타임 시 각각의 클래스 로더에 의해 생성된 클래스의 유일한 네임스페이스를 보장한다. 결과적으로, 애플리케이션은 서로 다른 버전의 라이브러리를 충돌 없이 사용할 수 있게 된다.

* 유일성의 원칙
	* 하위 클래스 로더가 상위 클래스 로더에게 로드한 클래스를 다시 로드하지 않아야 한다는 원칙
	* 위임 원칙에 의해서 위쪽으로 책임을 위임하기 때문에 고유한 클래스를 보장할 수 있음.

**동적 클래스 로딩**
* Class Loading 은 Class 참조 시점에 JVM에 코드가 링크되고, 실제 런타임 시점에 로딩되는 동적 로딩을 거침. 런타임에 동적으로 클래스를 로딩한다는 것은 JVM이 미리 모든 클래스에 대한 정보를 메소드 영역에 로딩하지 않는다는 것을 의미한다.
1. Load-time Dynamic Loading (로드 타임 동적 로딩)
```java
public class HelloWorld {
	public static void main(String[] args) {
		System.out.println("안녕하세요!");
	}
}
```
위 코드의 경우 다음과 같이 동작
* JVM 이 시작 되고 BootStrap Class Loader 가 생성된 후에 모든 클래스가 상속 받고 있는 Object 클래스를 읽어온다.
* Class Loader 는 명령 행에서 지정한 HelloWorld 클래스를 로딩하기 위해, HelloWorld.class 파일을 읽음
* HelloWorld 클래스를 로딩하는 과정에서 필요한 클래스인 java.lang.String 과 java.lang.System 을 로딩한다.
이처럼 하나의 클래스를 로딩하는 과정에서 동적으로 다른 클래스를 로딩하는 것을 로드 타임 동적 로딩이라고 한다.

2. Run-time Dynamic Loading(런타임 동적 로딩)
```java
public class RuntimeLoading {
	public static void main(String[] args) {
		try{
			Class cls = Class.forName(args[0]);
			Object obj = cls.newInstance();
			Runnable r = (Runnable) obj;
			r.run()
		}catch (Exception e) {
			e.printStackTrace();
		}
	}
}
```

Class.forName(className) 은 파라미터로 받은 className 에 해당하는 클래스를 로딩한 후에 객체를 반환하며, 다음과 같이 동작함.
* Class.forName() 메소드가 실행되기 전까지는 RuntimeLoading 클래스에서 어떤 클래스를 참조하는지 알 수 없다.
* 따라서 RuntimeLoading 클래스를 로딩할 때는 어떤 클래스도 읽어오지 않고, RuntimeLoading 클래스의 main() 메소드가 실행되고 Class.forName(args\[0\]) 을 호출하는 순간에 비로소 arg\[0\]에 해당하는 클래스를 로딩한다.

이 처럼 클래스를 로딩할 때가 아닌, 코드를 실행하는 순간에 클래스를 로딩하는 것을 런타임 동적 로딩이라고 한다.

#### Execution Engine

* Class Loader 에 의해 JVM 으로 Load 된 Class 파일(bytecode) 들은 Runtime Data Area의 Method Area 에 배치되는데, JVM 은 Method Area 의 바이트 코드를 Execution Engine 에 제공하여, Class 에 정의된 내용대로 바이트 코드를 실행시킨다. 이때, Load 된 bytecode를 실행하는 Runtime Module 이 Execution Engine 이다.

* 실행방식
	* 바이트코드를 명령어 단위로 읽어서 실행하는데, 두 가지 방식을 혼합사용
		* 1. Interpreter 방식
			* 바이트 코드를 한 줄씩 해석, 실행하는 방식. 초기 방식으로 한 줄씩 읽는거는 빠르지만 전체적으로 봤을 때는 느리다.
		* 2. JIT
			* 바이트코드를 JIT 컴파일러를 이용해 프로그램을 실제 실행하는 시점에 각 OS에 맞는 Native Code 로 변환하여 실행속도를 개선
			* 모든 코드를 JIT 컴파일러 방식으로 실행하지 않고, 인터프리터 방식을 사용하다 일정 기준이 넘어가면 JIT 컴파일러 방식으로 명령어를 실행한다.
			* 같은 코드를 매번 해석하지 않고, 컴파일을 하면서 캐싱해버린다.
			* 바뀐 부분만 컴파일하고 나머지는 캐싱된 코드를 사용


#### Runtime Data Area

![[Pasted image 20240401143301.png]]
_Java 는 Multi-Thread 환경으로 모든 Thread 는 Heap, Method Area 를 공유한다._

* PC Register
	* JVM 은 스택 기반의 가상 머신으로, CPU에 직접 접근하지 않고 Stack 에서 주소를 뽑아서 가져온다. 가져온 주소는 PC Register 에 저장된다.
	* 현재 어떤 명령을 실행하야 할 지에 대한 기록을 담당
* JVM Stacks
	* 호출된 메서드의 파라미터, 지역 변수, 리턴 값 및 연산 값 등이 저장되는 영역
	* 프로그램 실행 시 임시로 할당되었다가 메서드를 빠져나가게 되면 소멸되는 특성의 데이터들이 저장되는 영역
	* 메서드 호출 시마다 Stack 에 각각의 Stack 프레임이 생성되고, 수행이 끝나면 Stack 포인트에서 해당 프레임을 제거
* Frame 
	* 데이터, 반환 값을 저장하는 자료구조
	* 함수가 호출될 때 생성되고 함수가 종료되면 사라짐.
	* 각 프레임은 지역 변수 배열, Operand Stack, RunTime Constant Pool 에 대한 참조값을 지님.
	* 클래스파일의 함수에 대한 접근은 Runtime Constant Pool 에 존재하는 심볼릭 링크를 통해 접근 가능함.
	* 동적 할당은 코드 실행 시점에 심볼릭 링크를 해석해 고정된 주소값으로 변환시킴.
	* 심볼릭 링크를 통한 late-binding은 객체 지향의 핵심임.
* Native Method Stacks
	* Java 이외의 언어에 제공되는 Method 의 정보가 저장되는 공간/ Java Native Interface 를 통해 bytecode 로 저장
	* Kernel이 자체적으로 Stack 을 잡아 독자적으로 프로그램을 실행시키는 영역
* Heap
	* GC 의 대상이 되는 영역
	* 객체를 동적으로 생성하게 되면 인스턴스가 Heap 영역의 메모리에 할당됨.
	* 레퍼런스 변수의 경우(참조변수), Heap에 인스턴스가 저장되는 것이 아닌 포인터가 저장된다.
* Method Area
	* 클래스 정보를 처음 메모리에 올릴 때 초기화 되는 대상을 저장하기 위한 영역
	* 올라가는 정보
		* Field Information
			* 멤버 변수에 대한 정보(이름,타입,접근 지정자 등)
		* Method Information
			* 메서드에 대한 정보(이름, 리턴타입, 파라미터, 접근 지정자 등)
		* Type Information
			* Class 인지 Interface 인지 혹은 Type의 속성, 이름, super class 의 이름 등
			* Method Area에는 상수 형을 저장하고 중복을 막는 Runtime Constant Pool 이 존재
				* Runtime Constant Pool
					* 런타임 상수 풀 클래스, 인터페이스 마다 존재하며 클래스 파일의 constant pool 테이블 영역이 저장되는 공간
					* 각 클래스, 인터페이스의 전역 변수, 함수, 인스턴스 변수, 함수에 대한 심볼릭 링크가 존재한다.
					* 전역 변수와 전역 함수는 컴파일 시점에 할당되어 고정된 값으로 존재하며 인스턴스 변수와 인스턴스 함수는 심볼릭 링크로 존재하며 실행 시점에 고정된 주소로 변환된다.
					* 런타임 상수 풀은 클래스가 생성되어 Heap 에 할당될 때 만들어지며 클래스가 삭제되면 사라짐.

---
# GC 란?

Garbage Collector

* 자바 애플리케이션에서 사용하지 않는 메모리를 자동으로 수거하는 기능
* Heap 영역 에서 동적으로 할당했던 메모리 중 필요 없게 된 메모리 객체(garbage) 를 모아 주기적으로 제거 하는 프로세스를 말함.


## JVM 메모리 영역

_일반적으로 애플리케이션에서 사용되는 객체는 오래 유지되는 객체보다 잠시 사용되는 경우가 많음._
![[Pasted image 20240401181520.png]]
* Young Generation : 새롭게 생성하는 객체들이 존재하는 곳
* Old Generation : Young Generation 영역에서 오랫동안 살아남은 객체(가중치) 들이 존재하는 곳
* Meta Space : 클래스의 메타데이터, 문자열 정보를 저장하는 영역(JAVA 8 부터)
* YG 와 OG 로 나눈 이유는 애플리케이션에서의 객체의 수명은 대부분 짧기 때문에 효율적으로 관리하기 위함.

## GC 알고리즘

### Reference Counting
* Root Space 에 접근할 수 있는 방법(참조하는 곳)이 없는 객체는 삭제 대상이 됨.
* 순환참조에 대해 문제가 발생

### Mark-Sweep-Compact
_(아래에서 설명...)_
![[Pasted image 20240401181705.png]]
* JVM 에서 사용하는 방식
* Root Space 에서부터 순환을 하여 방문한 객체에 Mark 를 함.
  JVM에서 Root Space 는 stack, method stack, method 영역을 뜻함.
* Mark 가 되지 않은 객체, 즉 방문하지 않은 객체는 삭제(Sweep) 대상이 됨.
* 남아있는 객체들은 정리(Compact) 한다.
	Compact 는 필수가 아님. 의도적으로 GC 를 실행시켜야 되기 때문에 Stop The World가 발생한다.
![[Pasted image 20240401181931.png]]

* Stop The World
	GC 를 위해 어플리케이션을 일시적으로 멈추는 것


## JVM이 메모리를 관리하는 방식

### Heap 메모리의 구조

Heap 영역은 처음 설계될 때 다음의 2가지를 전제로 설계 되었음.
1. 대부분의 객체는 금방 접근 불가능한 상태가 된다.(Unreachable)
2. 오래된 객체에서 새로운 객체로의 참조는 아주 적게 존재한다.

➡️ 객체는 대부분 일회성이며, 메모리에 오래 남아있는 경우는 드물다.

* ***대부분의 객체는 금방 접근 불가능한 상태가 된다.**
![[Pasted image 20240402113722.png]]
	해당 이미지를 보면 알 수 있듯이 Young Generation 에서 Old Generation 으로 가는 객체들은 별로 없는것을 알 수 있다.
	이는 대부분의 객체는 금방 접근 불가능한 상태가 된다 라는 말과 같다.


* ***오래된 객체에서 새로운 객체로의 참조가 적다**
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

### GC 대상
![[Pasted image 20240401184813.png]]
_GC가 뭔데 할당된 메모리 회수함?_

GC 는 특정 객체가 garbage 인지 아닌지 판단하기 위해서 도달성, 도달 능력(Reachability) 라는 개념을 적용함.

객체에 레퍼런스가 있다면 Reachable 로 구분되고, 객체에 유효한 레퍼런스가 없다면 Unreachable 로 구분하고 수거한다.

* Reachable : 객체가 참조되고 있는 상태
* Unreachable : 객체가 참조되고 잇지 않은 상태(GC 의 대상)

_그래서 어떻게?_
![[Pasted image 20240401185745.png]]
#### Mark and Sweep
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
	* 자바 객체가 생성되자마자 저장되는 곳. 생성된 객체는 Minor GC 가 발생할 때 Survivor 영역으로 이동하게됨.
* Survivor
	* 해당 영역은 다시 survivor1, survivor2 로 나뉨.

**Minor GC 발생 시**
처음 생성된 객체는 YG 영역의 일부인 Eden 영역에 위치한다.
1. Eden 영역 꽉참 ➡️ Minor GC 실행
2. Mark 동작을 통해 reachable 객체를 탐색


이러한 방식은 속도가 매우 빠르며 작은 크기의 메모리를 콜렉팅하는데 매우 효과적이다.
Minor GC 의 경우에는 자주 일어나기 때문에 GC에 걸리는 시간이 짧은 알고리즘들이 적합함.

### Major GC (Old Generation GC, Full GC)

* Old 영역의 GC 를 Full GC 라고 부름. 여기서 사용되는 알고리즘을 Mark & Compact 라고 함.
* Mark & Compact 알고리즘은 객체들의 참조를 확인하면서 참조가 연결되지 않은 객체를 표시함. 이 작업이 끝나면 사용되지 않는 객체를 모두 표시하고 이 표시된 객체를 삭제함.
* Full GC 는 속도가 매우 느림. Full GC 가 일어나는 도중에는 순간적으로 자바 애플리케이션이 멈춰버리기 때문에, Full GC 가 일어나는 정도와 시간은 애플리케이션의 성능과 안정성에 아주 큰 영향을 미침.









### GC 의 Root Space

Mark and Sweep 방식은 루트로 부터 해당 객체에 접근이 가능한지가 해제의 기준이 됨.
JVM GC 에서의 Root Space 는 Heap 메모리 영역을 참조하는 method area, static 변수, stack, native method stack 이 되게 됨.











### GC 최적화
* 강한 참조(Strong Reference) : 기본적인 객체 참조 유형으로, 객체가 이러한 참조를 통해 접근 가능한 경우 GC 대상이 되지 않음.

* 약한 참조(Weak Reference) : 객체에 대한 약한 참조가 존재하는 경우, GC는 해당 객체를 회수할 수 있음. 약한 참조는 주로 캐시와 같이 메모리가 부족할 때 자동으로 해제될 수 있는 리소스에 사용됨.

* 소프트 참조(Soft Reference) : 약한 참조보다는 조금 더 강한 형태의 참조로, 메모리가 충분하지 않을 때에만 GC에 의해 회수 됨. 캐시 구현에 주로 사용됨.
  
* 팬텀 참조(Phantom Reference) : 참조 대상 객체가 GC 대상이 되어 회수되었음을 알리기 위해 사용됨. 직접적인 객체 접근용도로 사용되지는 않음.



---

**질문 : 왜 OS 에 종속되지 않는가?** 
컴파일 전 파일인 .java 는 CPU 가 인식하지 못하기 때문에 기계어로 컴파일을 해줘야합니다.
하지만 자바는 JVM 이라는 가상머신을 통해서 OS에 도달하기 때문에 OS가 인식할 수 있게 기계어로 바로 컴파일 되는게 아니라 JVM 이 인식할 수 있는 java bytecode 즉, .class 파일로 변환됩니다. bytecode 는 기계어가 아니기 때문에 OS에서 바로 실행되지는 않습니다. 이때 JVM 이 OS 가 bytecode 를 이해할 수 있도록 해석해 주기 때문에 bytecode 는 JVM 위에서 OS 상관없이 실행 될 수 있습니다.

**질문 : JVM 의 작동원리를 설명**
javac 로 컴파일 된 .java 파일을(.class 파일) Class Loader 가 로딩, 링크, 초기화를 한 뒤 Runtime data area 에 클래스 정보나 메타 데이터 등을 저장.
.class 파일을 Execution Engine 이 InterPreter 나 JIT Compiler 로 기계어로 번역 후 CPU가 실행

**질문 : 클래스 로더의 세가지 원칙**
위임, 가시성의 제한, 유일성 




JAVA BE 면접 질문 정리

# JAVA

1. JVM 에 대해서, GC의 원리
2. GC 의 종류
3. GC 선택 가이드원리
4. JAVA 메모리 영역
5. Collection
6. TreeSet, TreeMap ↔️ HashSet, HashMap
7. Array vs ArrayList & LinkedList
8. Annotation
9. Generic
10. static keyword
11. final keyword
12. Overriding vs Overloading
13. Access Modifier
14. Wrapper class Boxing 과 Unboxing, AutoBoxing
15. Checked & UnChecked Exception
16. Multi-Thread 환경에서의 개발
17. == 연산자, equals(), hashCode
18. Interface vs Abstract Class, Abstract method
19. 리플렉션이란?
20. Java Class 멤버 변수 초기화 순서
21. Java 버전별 특징 - 어느 버전에서 어떤 기능이 추가되었는지
22. OOP의 3대 조건과 5대 원칙
23. 좋은 객체 지향 프로그램이란

# Spring

1. Spring FrameWork의 핵심
	1. POJO 기반의 구성
	2. 제어의 역전(IoC)
	3. 의존성 주입
		1. DI 와 IoC
		2. DI 와 DIP
		3. 스프링에서의 의존성 주입이란
		4. 스프링에서는 어떻게 구현하는가?
		5. 왜 의존성 주입을 사용해야 하는가?
	4. DI 방식의 장단점
		1. 생성자(constructor) 주입
		2. 수정자(setter) 주입
		3. field 주입
	5. AOP(Aspect-Oriented Programming) 관점 지향 프로그래밍
	6. AOP 의 용어
	7. Spring Bean 이란?
	8. Spring Bean Scope
	9. Spring Bean LifeCycle
		1. Bean LifeCycle
		2. Bean LifeCycle CallBack
	10. Spring Container
	11. DL(Dependency LookUp) 이란?
2. SpringBoot 와 Spring 의 차이 (왜 Boot 를 쓸까?)
3. Controller로 들어오는 입력값에 대한 Validation 방법
4. Interceptor vs AOP vs Filter

---
실제 멘토님이 받은 면접 질문

# JAVA

1. GC 에 대해 설명
2. Interface 와 Abstract Class 차이
3. LinkedList 와 Abstract Class 의 차이
4. LinkedList 와 Array 차이
5. static keyword 란?
6. final keyword 란?
7. Overloading & Overriding
8. JAVA 에서 multi thread 구현 어떻게 하는지 & 장점
9. Java 11 특징
10. Boxing & UnBoxing
11. 리스코프 치환 원칙이란?

# Spring

1. SpringBoot 의 @Application Annotation 의 역할
2. DI - Spring 에서는 어떻게 구현하는지
3. Bean Scope
	1. Singletom
	2. Prototype
	3. Web
4. Bean LifeCycle
5. AOP

# DB

1. index 를 어떤 key에 설정하는지?
2. MySQL 에서 성능 확인을 위한 명령어
	* Explain
		* 실행 시 결과 값 중 어떤 값을 잘 봐야하는지?

# NetWork

1. HTTP Header
	* keep-alive header 란?
		* 왜 / 어떨 때 사용하는지?
	* TCP vs UDP
		* 3 ways handshake 란?
		* UDP 를 어떨때 사용?
	* OSI 7계층과 각 계층의 구성요소

# OS

* Process vs Thread
* DeadLock 이란?
* Non-Blocking 이란?

# Design Pattern

* 팩토리 패턴
* MSA
* EDA (Event Driven Architecture)

---



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

#### YG(young generation, not yg entertainment)
* 새롭게 생성된 객체가 할당(Allocation) 되는 영역
* 대부분의 객체가 금방 Unreachable 상태가 되기 때문에, 많은 객체가 Young 영역에 생성되었다가 사라짐.
* Young 영역에 대한 GC를 Minor GC 라고 부름.

#### OG(old generation, not original)
* Young 영역에서 Reachable 상태를 유지하여 살아남은 객체가 복사되는 영역
* Young 영역보다 크게 할당 되며, 영역의 크기가 큰 만큼 GC는 적게 발생
* Old 영역에 대한 GC를 Major GC 또는 Full GC 라고 부름
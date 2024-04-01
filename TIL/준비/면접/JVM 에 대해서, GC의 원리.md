---
sticker: emoji//1f3b0
---

# JVM 이란?

* Java Virtual Machine 의 줄임말
* OS 에 종속 받지 않고 CPU가 Java 를 인식, 실행할 수 있게 하는 가상 컴퓨터
* 또한 가장 중요한 메모리 관리, Garbage Collection 을 수행한다.

### 특징

1. 컴파일된 bytecode 를 기계가 이해할 수 잇는 기계어로 변환
2. 스택 기반의 가상머신
3. 메모리 관리와 GC 를 수행


### JVM 구조와 작동원리
![[Pasted image 20240401142940.png]]

JVM 구조에는 크게 Class Loader, Runtime Data Area, Execution Engine, GC 로 나누어져 있다.

**Class Loader** : 클래스 파일을 Runtime Data Area의 메서드 영역으로 불러오는 역할을 한다.

**Execution Engine** : .class 와 같은 bytecode 를 실행 가능하도록 해석한다.

**Runtime Data Area** : 런타임 시 클래스 데이터와 같은 메타 데이터와 실제 데이터가 저장되는 곳이다. Runtime Data Area 는 Method Area, Heap, PC Registers, Java Stacks, Native Method Stacks 로 나누어진다.

![[Pasted image 20240401143301.png]]
_Java 는 Multi-Thread 환경으로 모든 Thread 는 Heap, Method Area 를 공유한다._

* PC Register
	* JVM 은 스택 기반의 가상 머신으로, CPU에 직접 접근하지 ㅇ낳고 Stack 에서 주소를 뽑아서 가져온다. 가져온 주소는 PC Register 에 저장된다.
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









# GC 란?



---

**질문 : 왜 OS 에 종속되지 않는가?** 
컴파일 전 파일인 .java 는 CPU 가 인식하지 못하기 때문에 기계어로 컴파일을 해줘야합니다.
하지만 자바는 JVM 이라는 가상머신을 통해서 OS에 도달하기 때문에 OS가 인식할 수 있게 기계어로 바로 컴파일 되는게 아니라 JVM 이 인식할 수 있는 java bytecode 즉, .class 파일로 변환됩니다. bytecode 는 기계어가 아니기 때문에 OS에서 바로 실행되지는 않습니다. 이때 JVM 이 OS 가 bytecode 를 이해할 수 있도록 해석해 주기 때문에 bytecode 는 JVM 위에서 OS 상관없이 실행 될 수 있습니다.

**질문 : JVM 의 작동원리를 설명**

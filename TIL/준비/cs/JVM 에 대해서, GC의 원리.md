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


**클래스의 로딩, 초기화 시점 (싱글톤)** [링크](https://velog.io/@skyepodium/%ED%81%B4%EB%9E%98%EC%8A%A4%EB%8A%94-%EC%96%B8%EC%A0%9C-%EB%A1%9C%EB%94%A9%EB%90%98%EA%B3%A0-%EC%B4%88%EA%B8%B0%ED%99%94%EB%90%98%EB%8A%94%EA%B0%80)


* 클래스 로딩 시점
	* 클래스의 인스턴스 생성
	* 클래스의 정적변수 사용(final 키워드 x)
	* 클래스의 정적 메소드 호출
* 클래스가 로딩 하지 않을 때
	* 클래스에 접근하지 않을 때
	* 클래스의 정적 변수 사용(final 키워드 O)
* 초기화 시점
	* 클래스의 인스턴스 생성
	* 클래스의 정적변수 사용(final 키워드 X)
	* 클래스의 정적 메소드 호출
* 초기화 진행 순서
	* 정적 블록
	* 정적 변수
	* 생성자

* 한 번만 클래스가 로딩됨을 보장
	* JLS 에 따르면 JVM 에 클래스가 로딩되고 초기화될 때는 순차적으로 동작함을 보장한다. 멀티 스레드 환경에서 여러 개의 스레드가 동시에 클래스를 로딩하려고 하면 오직 한 개의 클래스만 로딩된다.
* singleton
	* Initialization-on-demand holder idiom 방식(holder 에 의한 초기화 방식) 을 사용하면 클래스 로딩 및 초기화 과정이 스레디 safe 하다는 것을 이용하여 싱글톤 인스턴스를 생성할 수 있음. 이 패턴이 가장 완벽하다고 평가 받음.
```java
//Holder 에 의한 초기화 방식
public class HolderSingletom {
	private HolderSingleton() {
	}
	public static HolderSingleton getInstance() {
		return Holder.instance;
	}
	private static class Holder {
		public static final HolderSingleton instance = new HolderSingleton();
	}
}
```
	
```java
//Eager Initialization (이른 초기화 방식)
public class Singleton {
	public static final Signleton instance = new Singleton();
	
	private Singleton() {
	}

	public static Singleton getInstance() {
		return instance;
	}
}
```
이 방식은 singleton 클래스가 로딩될 때 사용하지 않을 수도 있는 instance 변수(싱글톤 객체) 가 생성되기 때문에 메모리가 낭비됨.


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

최종적으로 java 파일을 실행 시킬 때

1. 소스 컴파일
	Java 소스 파일(.java) 는 javac 에 의해 bytecode 로 컴파일 됨.
	이 bytecode 는 .class 파일에 저장되며, 이 파일은 JVM 이 이해하고 실행할 수 있는 중간 표현 형태
1. 클래스 로딩
	실행 시 Class Loader는 .class 파일들을 JVM 내로 로드. Class Loader는 동적으로 필요한 클래스들을 찾아 메모리에 로드하는 역할을 함.
2. 검증
	로드된 클래스 파일이 올바른 형식을 가지고 있고, 안전하게 실행될 수 있는지 검증한다. 이 과정은 bytecode 검증기를 통해 수행되며, 메모리 손상, 스택 오버플로우 등의 보안 문제를 예방.
3. 준비
4. 해석
5. 초기화
6. 실행 (Runtime Data Area 할당)
7. 실행 (Execution Engine)
8. 실행 (CPU)









# GC 란?



---

**질문 : 왜 OS 에 종속되지 않는가?** 
컴파일 전 파일인 .java 는 CPU 가 인식하지 못하기 때문에 기계어로 컴파일을 해줘야합니다.
하지만 자바는 JVM 이라는 가상머신을 통해서 OS에 도달하기 때문에 OS가 인식할 수 있게 기계어로 바로 컴파일 되는게 아니라 JVM 이 인식할 수 있는 java bytecode 즉, .class 파일로 변환됩니다. bytecode 는 기계어가 아니기 때문에 OS에서 바로 실행되지는 않습니다. 이때 JVM 이 OS 가 bytecode 를 이해할 수 있도록 해석해 주기 때문에 bytecode 는 JVM 위에서 OS 상관없이 실행 될 수 있습니다.

**질문 : JVM 의 작동원리를 설명**
javac 로 컴파일 된 .java 파일을(.class 파일) Class Loader 가 가져와서 검증, 링크, 초기화를 한 뒤 Execution 

**질문 : 클래스 로더의 세가지 원칙**

**질문 : 클래스 로더가 어떻게 클래스를 동적으로 로딩하는지?**

**질문 : 클래스 로딩 시점**

**질문 : 클래스 초기화 시점**

**질문 : 싱글톤 패턴과 클래스로더는 어떤 연관이 있는지?**



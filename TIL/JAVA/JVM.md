**Java Virtual Machine** 이란

자바 가상 머신

Java 를 어느 환경에서도 동작 시키기 위한 가상의 컴퓨터

Java 는 인터프리터 언어가 아니여서 사람이 작성한 코드를 바이트코드로 변환하는 작업을 한다.

*.java 파일을 *.class 파일로 변환하여 컴퓨터(CPU)가 인식할 수 있게 한다.

*.java 파일을 *.class 로 변환하는 녀석은 Java Complier 가 하고 있다.(_jdk를 설치하면 있는 javac라는 녀석)_

하지만 이렇게 변환된 녀석은 기계어가 아니기 때문에 OS에서 바로 실행 되지는 않는다.

컴파일 언어는 OS 마다 실행할 수 있는 기계어가 다른 경우가 있기 때문에 OS에 맞는 기계어로 다시 변경을 해줘야한다.

이때 JVM이 OS 가 바이트코드를 이해할 수 있도록 한다.

### 바이트코드..

**특정 하드웨어가 아닌 가상 컴퓨터에서 돌아가는 실행 프로그램을 위한 이진 표현법**

Java bytecode는 JVM에서 돌아가기 위해 변환된 자바코드이다.

Java bytecode 는 자바 프로그램을 배포하는 가장 작은 단위

바이트코드는 JIT 컴파일러에 의해 바이너리 코드로 변환된다.

_**binary code** : 텍스트, 컴퓨터 프로세서 명령 또는 그 밖의 2심볼 시스템을 사용하는 데이터를 대표하며 대개 이진 숫자 체계의 0과 1을 의미_

### JIT Compiler

런타임 시 기본 시스템 코드로 바이트 코드를 컴파일하여 Java 애플리케이션의 성능을 향상 시키는 런타임 환경의 컴포넌트 ⇒ 프로그램을 실제 실행하는 시점에 기계어로 번역하는 컴파일러

**인터프리터 방식의 단점을 보완하기 위해 도입됨.**

⇒ 인터프리터 방식으로 실행하다가 적절한 시점에 바이트 코드 전체를 컴파일하여 기계어로 변경, 이후에는 더 이상 인터프리팅 하지 않고 기계어로 직접 실행하는 방식

Java Compiler(javac) ⇒ *.java → *.class(bytecode) 변환 ⇒ JVM(JIT Compiler) ⇒ 기계어 순서라고 보면됨.

### **JVM 구조**

![[Pasted image 20231019094924.png]]

- **클래스로더**
- **실행엔진**
    - **인터프리터**
    - **JIT 컴파일러**
    - **GC**
- **런타임 데이터 영역**

### 클래스로더

1. 로딩 : 클래스를 로딩... 로딩 완료시 링크를 함.
    
2. 링크
    
    1. Verify: .class 파일 형식이 유요한지 검증
        
    2. Prepare: 클래스 변수(static 변수) 와 기본값에 필요한 메모리
        
    3. Resolve : 심볼릭 메모리 레퍼런스를 메소드 영역에 있는 실제 레퍼런스로 교체한다.
        
    
    - 심볼릭 레퍼런스 : 실제 new 로 해서 생성한 객체는 클래스 로딩 전에 실제 힙영역에 있는 객체를 참조하지 않는다. 논리적(?)으로 참조하고 있는 것이다. 하지만 Resolve 단계에서 이 논리적인 참조를 힙 영역과 연결하는 역할을 한다.
3. 초기화 : static 변수의 값을 할당한다. 클래스의 static 키워드가 붙은 것들은 이때 할당이 된다.
    

### 실행엔진

1. 인터프리터 : 바이트 코드를 이해하는 것. 기계언어로 한줄 씩 바꿔준다. 한줄마다 네이티브 코드로 컴파일 한다. 똑같은 코드가 나올때는 JIT 컴파일러로 보낸다.
2. JIT 컴파일러 : 저스트 인 타임 컴파일러. 자바 파일을 컴파일 하는 것이 아니라 바이트코드를 네이티브 코드로 바꾼다. 반복된 코드를 다 찾아서 미리 바꿔 놓는다. 인터프리터가 반복하는 코드에 진입했을 때 한줄 씩 인터프린팅 하는 것이 아니라 변경되어 있는 네이티브 코드를 바로 실행한다.
3. GC(가비지 컬렉터) : 안쓰는 객체들을 없애는 역할

### **런타임 데이터 영역**

JVM 이 프로그램을 수행하기 위해 OS 로 부터 할당받는 메모리영역.

WAS 의 성능 문제 발생 시, 해당 부분이 원인이 되는 경우가 많다.

**PC Register**

Thread 마다 생성

Thread가 어떤 부분을 어떤 명령으로 실행해야할 지에 대한 기록을 하는 부분으로 현재 수행 중인 JVM 명령의 주소를 가짐

**JVM 스택 영역**

쓰레드마다 런 타임 스택 생성. 그 안에다가 스택 프레임을 쌓는다.

(메소드 콜, 어떤 메소드를 호출 했는지), Exception 또는 Error 시 나오는 콘솔창에 쓰레드마다 한개 씩 생성됨.

**네이티브 메소드 스택**

네이티브 메소드를 호출 할 때 메소드에 native라는 키워드가 있고 그 메소드의 구현을 C 또는 C++로 한 것.

실제로 Thread.currentThread();를 까서 들어가보면 native 키워드가 붙어 있는게 있다.

**메서드 영역**

클래스 수준의 정보, 전역적으로 사용되는 공유자원 느낌.

- 풀패키지 경로 ( package me.mypackage; 클래스 맨위에 있는..)
- 클래스 이름
- 상속받은 클래스가 있다면 부모클래스의 이름
- 스태틱 변수 ( static int number = 10;)
- 메서드 들

**Heap**

객체 저장, 인스턴스들을 명시적으로 만드는 객체들도 힙에 저장됨.

(ex) Person person = new Person();
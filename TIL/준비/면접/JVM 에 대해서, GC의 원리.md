
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

**Class Loader** : 클래스 파일을 Run


# GC 란?



---

**질문 : 왜 OS 에 종속되지 않는가?** 
컴파일 전 파일인 .java 는 CPU 가 인식하지 못하기 때문에 기계어로 컴파일을 해줘야합니다.
하지만 자바는 JVM 이라는 가상머신을 통해서 OS에 도달하기 때문에 OS가 인식할 수 있게 기계어로 바로 컴파일 되는게 아니라 JVM 이 인식할 수 있는 java bytecode 즉, .class 파일로 변환됩니다. bytecode 는 기계어가 아니기 때문에 OS에서 바로 실행되지는 않습니다. 이때 JVM 이 OS 가 bytecode 를 이해할 수 있도록 해석해 주기 때문에 bytecode 는 JVM 위에서 OS 상관없이 실행 될 수 있습니다.

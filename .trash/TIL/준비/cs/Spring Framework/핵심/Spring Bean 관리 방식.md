
### Spring Bean 관리 방법


Spring Framework 는 Bean 을 관리하기 위해 IoC(Inversion of Control) 컨테이너를 사용함.

Spring IoC 컨테이너는 애플리케이션의 구성 및 종속성 관리를  담당함.


* **Bean 정의**
	* XML 파일, Java 어노테이션, 또는 Java 설정 클래스(Java Config) 를 사용하여 Bean 을 정의함.
* **Container 초기화**
	* Spring IoC 컨테이너는 설정 파일 또는 클래스에 정의된 Bean 들을 로드하고 인스턴스를 생성함.
* **의존성 주입**
	* 컨테이너는 Bean 간의 의존성을 해결하고 필요한 경우 의존성을 주입함. 이 때 생성자 주입, Setter 주입, 또는 Field 주입을 사용할 수 있음.
* **Bean 라이프 사이클 관리**
	* 컨테이너는 Bean 의 생성 초기화, 소멸 등 라이프사이클을 관리함. 이를 위해 `@PostContruct`와 `@PreDestroy` 어노테이션 등을 사용할 수 있음.


### 관리에 사용되는 자료구조

Spring IoC 컨테이너는 Bean 을 저장하고 관리하기 위해 다양한 자료구조를 사용함. 대표적인 자료구조는 다음과 같음.

* `ConcurrentHashMap`
	* 대부분의 경우 Spring 은 Bean 이름(또는 ID) 과 Bean 인스턴스를 매핑하기 위해 `ConcurrentHashMap` 을 사용함. 이 자료조는 동시성을 지원하므로 다중 스레드 환경에서 안전하게 Bean 을 관리할 수 있음.
* `List` 및 `Set`
	* Bean 정의를 저장하거나 초기화 후 호출해야 하는 작업 목록을 관리하기 위해 사용됨. `List` 는 순서가 주용한 경우, `Set` 은 순서가 중요하지 않은 경우 사용됨.
* `ArrayList`
	* 특정 시점에서 초기화된 Bean 의 순서를 유지하기 위해 사용될 수 있음.
* `LinkedHashMap`
	* 정의된 순서대로 Bean 을 관리해야 할 경우 사용됨.

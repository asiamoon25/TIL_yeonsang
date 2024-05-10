`Interceptor` , `AOP`, `Filter` 는 모두 Java 기반 웹 및 엔터프라이즈 애플리케이션에서 사용되는 기술임.
요청/응답 처리나 메서드 실행을 가로채는 방식으로 횡단 관심사를 처리함.

각각의 기술의 목적, 특징 및 실행 영역이 다름.

## Interceptor vs AOP vs Filter

### Interceptor

* 목적
	특정 요청이나 메서드 호출을 가로채어 전처리 및 후처리 로직을 수행 

* 특징
	* Spring MVC 에서는 Controller 호출 전후로 요청을 가로채는 `HandlerInterceptor` 를 제공함.
	* Java EE/EJB 에서는 비즈니스 메서드 호출 전후로 동작하는 EJB Interceptor 를 제공함.
	* Hibernate 에서는 엔티티 변경 전후로 동작하는 `Interceptor` 가 있음.

* 영역 및 단위
	* Spring MVC : HTTP 요청/응답 처리 영역
	* Java EE/EJB : 비즈니스 메서드 실행 영역
	* Hibernate : 엔티티 변경 영역


### AOP

* 목적
	메서드 호출 전후 및 예외 발생 시 등 다양한 시점에서 횡단 관심사를 처리할 수 있는 패러다임 제공

* 특징
	* `Aspect`, `Advice`, `Pointcut`, `JoinPoint` 등의 개념을 통해 구현함.
	* Spring AOP 와 AspectJ 프레임워크에서 주로 사용됨.

* 영역 및 단위
	* 메서드 호출 및 클래스/메서드/ 필드 조합 등의 세밀한 단위에서 실행
	* 주로 비즈니스 로직 전후의 횡단 관심사 처리


### Filter

* 목적 
	HTTP 요청/응답 을 가로채어 전처리 및 후처리 로직을 수행함.

* 특징
	* Servlet Container 수준에서 동작하며 모든 HTTP 요청 및 응답에 대해 전역적으로 작동함.
	* `javax.servlet.Filter` 인터페이스를 구현하여 사용함.

* 영역 및 단위
	* Servlet Container 수준에서 HTTP 요청/응답 단위로 동작

|특징|Interceptor|AOP|Filter|
|---|---|---|---|
|**목적**|요청/응답 또는 메서드 호출 전후 처리|횡단 관심사 처리|HTTP 요청/응답 전후 처리|
|**사용 계층**|Spring MVC, Java EE, Hibernate|Spring AOP, AspectJ|서블릿 컨테이너|
|**단위**|요청/응답, 메서드 호출 단위|메서드 호출 단위|HTTP 요청/응답 단위|
|**구현**|인터페이스 및 애너테이션|애너테이션 및 POJO 클래스|`Filter` 인터페이스 구현|
|**적용 대상**|컨트롤러, 비즈니스 메서드, 엔티티|비즈니스 메서드, 클래스|HTTP 요청 및 응답|
|**실행 시점**|요청 전후, 메서드 호출 전후|메서드 호출 전후, 예외 처리 시|HTTP 요청 전후|

- **Interceptor**: 컨트롤러나 메서드 호출을 가로채어 전처리 및 후처리 로직을 수행한다.
- **AOP**: 메서드 호출, 예외 발생 등 다양한 시점에서 횡단 관심사를 처리하는 프로그래밍 패러다임.
- **Filter**: 서블릿 컨테이너에서 모든 HTTP 요청/응답을 가로채어 전처리 및 후처리 로직을 수행한다.
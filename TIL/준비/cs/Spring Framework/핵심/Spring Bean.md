---
sticker: lucide//bean
---
* Index
	* Spring Bean 이란?
		* 왜 사용함?
			* 중요 이유
	*  Spring Bean Scope
		1. Spring Bean LifeCycle
			1) Bean LifeCycle
			2) Bean LifeCycle CallBack



## Spring Bean 이란?

* Framework가 관리하는 객체를 의미
* 스프링 컨테이너에 의해 관리되는 재사용 가능한 소프트웨어 컴포넌트
* Spring IoC(Inversion of Control) 컨테이너에 의해 인스턴스화, 관리, 설정됨.
* 애플리키에션의 핵심을 이루는 비즈니스 로직, 데이터베이스 연결, 인프라 서비스 등을 담당.

_new 키워드 대신 스프링이 알아서 해줌._


### 왜 사용함?

Spring Framework 의 핵심 기능인 의존성 주입(Dependency Injection, DI) 을 효과적으로 활용하기 위해서임.

스프링 빈과 관련된 기능들은 애플리케이션 개발을 단순화 하고, 코드의 모듈성을 높이며, 유지보수를 용이하게 하는 데 중요한 역할을함.

#### 중요이유

1. **모듈성과 분리**
	스프링 빈을 사용하면 애플리케이션의 다양한 부분을 잘 정의된 컴포넌트로 나눌 수 있음. 
	각 컴포넌트는 스프링 빈으로 등록되어 서로 독립적으로 작동할 수 있으며, 필요한 의존성만 주입받아 사용함. 
	➡️ 코드의 결합도를 낮추고, 각 컴포넌트의 재사용성과 테스트 용이성을 향상시킴.

2. **유연한 의존성 관리**
	스프링의 의존성 주입 기능은 컴포넌트 간의 의존성을 외부에서 관리할 수 있게 해줌.
	개발자가 직접 객체를 생성하고 관리하는 대신, 스프링 컨테이너가 라이프사이클과 의존성을 자동으로 처리해주어, 더 깔끔하고 유지보수가 용이한 코드를 작성할 수 있게 해줌.

3. **설정과 코드의 분리**
	스프링 빈의 설정은 보통 xml 파일이나 Java 기반의 설정 클래스에서 이루어짐.
	설정을 코드에서 분리함으로써, 애플리케이션 로직과 설정 사이의 역할을 명확히 할 수 있고, 변경 사항을 적용하기 더 간편해짐.

4. **라이프사이클 관리**
	스프링 컨테이너는 빈의 전체 라이프사이클을 관리함. 개발자는 빈이 생성되고, 의존성이 주입된 후 필요한 초기화 작업을 수행할 수 있으며, 애플리케이션이 종료될 때 청소(clean-up) 작업을 수행할 수 있음.

5. **AOP 지원**
	스프링 빈은 AOP를 자연스럽게 지원함.
	이는 트랜젝션 관리, 보안, 로깅 등의 교차 관심사를 비즈니스 로직에서 분리하여 관리할 수 있도록 도와줌.

6. **향상된 테스트 가능성**
	의존성 주입을 통해, 테스트 중에 컴포넌트의 실제 의존성을 모의객체 로 쉽게 대체할 수 있음. 이는 단위테스트의 복잡성을 줄이고, 더 높은 품질의 자동화된 테스트를 가능하게 함.


## Spring Bean Scope

Bean 의 scope 는 해당 Bean 인스턴스의 생명 주기와 가시성을 정의함.

* `Singleton` : 기본값으로, Spring IoC 컨테이너당 단 하나의 Bean 인스턴스만 생성됨.
* `Prototype` : 요청할 때마다 새로운 Bean 인스턴스가 생성됨.
* `Request` : HTTP 요청당 하나의 Bean 인스턴스가 생성됨. 주로 웹 애플리케이션에서 사용됨.
* `Session`  : HTTP 세선당 하나의 Bean 인스턴스가 생성됨.
* `Global Session` : 포털 애플리케이션에서 사용되며, 전역 HTTP 세션당 하나의 Bean 인스턴스가 생성됨.


### Spring Bean LifeCycle

Spring Bean 의 생명주기는 크게 생성 및 초기화 단계, 사용 및 호출 단계, 그리고 소멸단계로 나뉨.

#### Bean LifeCycle
1. `Bean 정의 읽기` : XML 파일, Java Config 등에서 Bean 정의를 로드함.
2. `Bean 인스턴스화` : 정의된 클래스의 인스턴스를 생성함.
3. `의존성 주입` : Bean 이 필요로 하는 의존성들을 주입함.
4. `Bean 초기화` : Bean 이 생성되고, 의존성이 주입된 후에 초기화를 수행함. 여기서 사용자가 커스텀 초기화로 로직을 구현할 수 있음.
5. `Bean 사용` : 애플리케이션에서 Bean 을 사용함.
6. `Bean 소멸` : 컨테이너가 종료될 때 Bean 을 소멸 시키며, 여기서도 커스텀 소멸로 로직을 구현함.


#### Bean LifeCycle CallBack

Bean 의 생명주기 중 특정 이벤트에 대해 커스텀 로직을 실행할 수 있는 방법

* `InitializingBean / DisponsableBean` : 빈이 초기화 / 소멸될 때 `afterPropertiesSet()` 및 `destroy()` 메소드를 오버라이드해서 사용할 수 있음.
* `@PostConstruct / @PreDestroy 어노테이션` : 이 어노테이션을 메소드에 적용하여 초기화 및 소멸 시 호출되도록 할 수 있음.
* `xml 의 init-method / destroy-method` : XML 설정에서 직접 메소드를 지정하여 초기화 및 소멸 시 호출 되게 설정할 수 있음.



**예시 코드**

```java
import org.springframework.beans.factory.DisposableBean;
import org.springframework.beans.factory.InitializingBean;
import javax.annotation.PostConstruct;
import javax.annotation.PreDestroy;

public class ExampleBean implements InitializingBean, DisposableBean {
    private String value;

    // Constructor
    public ExampleBean(String value) {
        this.value = value;
        System.out.println("Constructor called: Bean is created with value=" + value);
    }

    // PostConstruct
    @PostConstruct
    public void initPostConstruct() {
        System.out.println("@PostConstruct: After properties are set");
    }

    // Implementing InitializingBean
    @Override
    public void afterPropertiesSet() throws Exception {
        System.out.println("InitializingBean: afterPropertiesSet method called");
    }

    // Custom init method
    public void customInit() {
        System.out.println("Custom INIT method called");
    }

    // PreDestroy
    @PreDestroy
    public void preDestroy() {
        System.out.println("@PreDestroy: Before bean is destroyed");
    }

    // Implementing DisposableBean
    @Override
    public void destroy() throws Exception {
        System.out.println("DisposableBean: destroy method called");
    }

    // Custom destroy method
    public void customDestroy() {
        System.out.println("Custom DESTROY method called");
    }
}
```


XML 설정에서 init-method 와 destroy-method 를 사용하려면 다음과 같이 할 수 있음.

```xml
<bean id="exampleBean" class="ExampleBean" init-method="customInit" destroy-method="customDestroy">
    <constructor-arg value="Initial value"/>
</bean>
```

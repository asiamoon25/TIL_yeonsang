
## DL 이란?
* Dependency LookUp
* 의존성 검색
* 필요한 시점에 직접 Spring Bean 에 접근하기 위해 컨테이너가 제공하는 API 를 이용하여 LookUp 하는 것
* DI 와 비슷하게 두 방식 모두 의존성 관리와 객체간의 결합도를 낮추는 데 목적이 있음.

## Spring FrameWork에서의 Dependency LookUp

Spring Framework 는 의존성 주입(DI)을 주로 사용하지만, Dependency Lookup 패턴도 지원함. Spring 에서 Dependency Lookup 을 사용할 때는 주로 `ApplicationContext` 를 사용하여 명시적으로 Bean 을 검색함.

### ApplicationContext

```java
ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");

MyBean bean = context.getBean("myBean", MyBean.class);
```

코드 내에서 `ApplicationContext` 를 직접 주입받은 후에 사용하기 때문에 Spring이 추구하는 POJO 개발인데, 이 방식은 스프링에 종속적이게 됨.

### ObjectProvider

ObjectProvider 는 ObjectFactory를 상속받은 interface 로 `getObject` 메서드를 통해 DL 을 제공함.




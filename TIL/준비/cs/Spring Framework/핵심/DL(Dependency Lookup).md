
## DL 이란?
* Dependency LookUp
* 의존성 검색
* 필요한 시점에 직접 Spring Bean 에 접근하기 위해 컨테이너가 제공하는 API 를 이용하여 LookUp 하는 것
* DI 와 비슷하게 두 방식 모두 의존성 관리와 객체간의 결합도를 낮추는 데 목적이 있음.

## Spring FrameWork에서의 Dependency LookUp

Spring Framework 는 의존성 주입(DI)을 주로 사용하지만, Dependency Lookup 패턴도 지원함. Spring 에서 Dependency Lookup 을 사용할 때는 주로 `ApplicationContext` 를 사용하여 명시적으로 Bean 을 검색함.

### ApplicationContext

`ApplicationContext` 는 Spring 의 중심 컴포넌트로, 애플리케이션 전반에 걸쳐 Bean 관리, 의존성 주입, 설정 등을 담당하는 컨테이너임.
이 컨텍스트는 빈의 정의, 생성, 그리고 관리를 수행하며, 애플리케이션의 구성 요소들 간의 생명주기를 조절함.

**특징**
* **빈 생명주기 관리**
	객체의 생성, 초기화, 소멸 과정을 관리함.
* **이벤트 발행**
	애플리케이션 이벤트를 발행하고, 이벤트 리스너를 통해 이벤트를 처리함.
* **국제화 지원**
	메시지 소스를 통해 다국어 애플리케이션을 지원함.
* **환경 추상화**
	프로파일과 프로퍼티를 통해 다양한 환경에서 애플리케이션을 유연하게 구성할 수 있음.
* **빈 검색**
	특정 타입이나 ID 를 기준으로 빈을 검색할 수 있음.

```java
ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");

MyBean bean = context.getBean("myBean", MyBean.class);
```


### ObjectProvider

`ObjectProvider` 는 `ApplicationContext` 의 기능을 좀 더 유연하게 확장한 래퍼로써, 특정 빈의 지연 로딩이나 선택적 검색을 용이하게 만들어줌.

`ObjectProvider` 는 `ApplicationContext` 에서 빈을 직접 요청하는 대신, 필요할 때까지 빈의 생성을 지연시키거나, 조건에 따라 빈을 선택적으로 가져올 수 있도록 도와줌.

**특징**
* **지연 로딩**
	빈의 존재 여부나 타입에 따라 지연 로딩을 할 수 있어, 의존성을 유연하게 관리할 수 있음.
* **조건적 접근**
	주어진 타입의 빈이 여러 개 있을 때, 특정 조건에 맞는 빈을 획득할 수 있음.
* **기능성 인터페이스**
	`ObjectProvider` 는 `getIfAvailable()` 및 `getIfUnique()` 메서드를 제공하여 빈의 존재 유무에 따라 처리 방식을 다르게 할 수 있음.

```java
@Component
public class MyComponent {
	private final MyBean myBean;
	
	@Autowired
	public MyComponent(ObjectProvider<MyBean> beanProvider) {
		this.myBean = beanProvider.getIfAvailable(() -> new MyBean());
	}
}
```




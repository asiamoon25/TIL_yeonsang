---
sticker: emoji//2622-fe0f
---
#spring 


## IoC(Inversion of Control) 

### **제어의 역전이란**
* 소프트웨어 설계 원칙 중 하나로 프로그래밍에 있어 객체의 생성 및 관리 책임을 개발자에서 전체 애플리케이션 또는 프레임워크에 위임하는 디자인 원칙을 말함.
* 일반적으로 객체의 생성과 그 객체 간의 의존성 결합에 관한 제어권이 개발자에서 프레임워크로 넘어가게된다.


### 제저의 역전의 구성 요소

#### 의존성 주입
* 객체가 필요로 하는 의존성 외부에서 주입받는 방식을 사용.
* 의존성 주입은 생성자 주입, 세터 주입, 필드 주입 등 다양한 방법으로 수행될 수 있음.

**생성자 주입**
* 생성자 주입은 생성자를 통해 의존성을 주입받는 방법임. 이 방식은 의존성이 필수적일 때 주로 사용됨.

```java
import org.springframework.stereotype.Component;

@Component
public class BookService {
	private final BookRepository bookRepository;
	// 생성자를 통한 의존성 주입
	public BookService(BookRepository bookRepository) {
		this.bookRepository = bookRepository;
	}
	public void processBook() {
		bookRepository.save(new Book());
	}
}
```

**Setter Injection(생성자 주입)**
* Setter 주입은 객체 생성 후 세터 메서드를 통해 의존성을 주입받는 방식. 이 방식은 의존성이 선택적일 때 유용함.

```java
import org.springframework.beans.factory.annotation.Autowired; 
import org.springframework.stereotype.Component;

@Component
public class MemberService {
	private MemberRepository memberRepository;
	
	//setter를 통한 의존성 주입
	@Autowired
	public void setMemberRepository(MemberRepository memberRepository){
		this.memberRepository = memberRepository;
	}
	
	public void registerMember() {
		memberRepository.save(new Member());
	}
}
```


**Field Injection 필드 주입**
* 필드 주입은 필드 선언에 직접 `@Autowired` 어노테이션을 사용하여 의존성을 주입받는 방법임.
* 간단하지만 테스트와 변경에 어려움이 있을 수 있음.

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;

@Component
public class UserService {
    @Autowired
    private UserRepository userRepository;

    public void addUser() {
        userRepository.save(new User());
    }
}
```


>의존성 주입이 제대로 이루어졌는지 확인하는 방법은 다양함.
>
일반적으로 스프링 애플리케이션을 실행하면서 해당 빈이 제대로 생성되고 주입되었는지 로그를 통해 확인 할 수 있음.
>
또한, 통합 테스트나 단위 테스트를 작성하여 의존성이 올바르게 주입되었는지 검증할 수 있음.
>
>단위 테스트에서는 Mockito 와 같은 모킹 툴을 사용하여 의존성을 명시적으로 주입하고 그 효과를 검증하기도 함.

#### 빈(Bean)

* 스프링에서 객체를 빈이라고 부르며, 스프링 IoC 컨테이너가 관리하는 객체임.
* 빈의 생명주기와 의존성은 컨테이너에 의해 관리됨.

1. **어노테이션을 통한 빈 정의**
	가장 흔이 사용되는 방법 중 하나는 컴포넌트 스캐닝 기능을 사용하는 것임.
	`@Component` 및 이를 확장한 `@Service`, `@Repository`, `@Controller` 등의 어노테이션을 사용하여 클래스를 빈으로 등록할 수 있음.

```java
import org.springframework.stereotype.Component;

@Component  // 빈 등록
public class ExampleService {
    public void serve() {
        System.out.println("Service is running...");
    }
}
```

2. xml 을 통한 빈 정의
	xml 파일 내에서 빈을 선언하면 스프링 컨테이너가 해당 빈을 인스턴스화 하고 관리함.

```xml
<beans ...>
  <bean id="MyService"
        class="com.example.my.MyService">
    <property name="myRepository"
              ref="myRepository"/>
  </bean>
  <bean id="MyRepository"
        class="com.example.my.MyRepository">
  </bean>
</beans>
```

3. Java 기반 설정을 통한 빈 정의
	스프링 3.0 부터는 자바 기반의 설정을 사용하여 빈을 정의할 수 있음.
	이 방법은 `@Configuration` 어노테이션에 붙은 클래스 내에서 `@Bean` 어노테이션을 사용하여 메서드 레벨에서 빈을 정의함.

```java

```





**컨테이너(Container)**
	스프링 IoC 컨테이너는 설정 정보를 바탕으로 객체를 생성하고, 관리하며, 의존성을 주입하는 역할을 함. 컨테이너는 애플리케이션의 구성 요소들을 초기화, 생성, 조립하는 책임을 담당함.
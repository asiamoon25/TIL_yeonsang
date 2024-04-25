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



빈(Bean)
	스프링에서 객체를 빈이라고 부르며, 스프링 IoC 컨테이너가 관리하는 객체임.
	빈의 생명주기와 의존성은 컨테이너에 의해 관리됨.

**컨테이너(Container)**
	스프링 IoC 컨테이너는 설정 정보를 바탕으로 객체를 생성하고, 관리하며, 의존성을 주입하는 역할을 함. 컨테이너는 애플리케이션의 구성 요소들을 초기화, 생성, 조립하는 책임을 담당함.
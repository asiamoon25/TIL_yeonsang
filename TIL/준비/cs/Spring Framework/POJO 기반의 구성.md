---
sticker: emoji//1f4fd-fe0f
---
## POJO 기반의 구성

### POJO 란?
* Plain Old Java Object 의 약자
* 특정 규약이나 프레임워크, 클래스를 상속받지 않는 간단한 Java 객체를 말함.
* Serializable 인터페이스 처럼 최소한의 Java 표준을 따르며, 특정 인터페이스를 구현하거나 클래스를 확장하지 않고도 자유롭게 작성될 수 있음.
```java
public interface MessageService {
	String getMessage();
}

public class SimpleMessageService implements MessageService {
	@Override
	public String getMessage() {
		return "Hello, Spring framework"
	}
}
```

위 `MessageService` 는 인터페이스이며, `SimpleMessageService` 는 이 인터페이스를 구현하는 POJO 임. `SimpleMessageService` 는 특별한 의존성이 없고, Spring의 API에 의존하지 않음.
## 왜 필요함?

1. 단순성
	POJO 는 특정 기술에 종속되지 않기 때문에 이해하기 쉽고, 유지 관리가 간편함.

2. 테스트 용이성
	POJO 는 독립적인 구조를 가지므로, Spring 과 같은 컨테이너 환경을 구성하지 않고도 단위 테스트가 가능

3. 재사용성 및 확장성
	POJO 를 사용함으로써 다른 Java 애플리케이션에서도 재사용할 수 있으며, 변경 사항이 있을 때 다른 부분에 영향을 미치지 않고 수정이 가능함.

4. 경량성
	POJO 는 가벼우므로 애플리케이션의 성능 부담을 줄입니다.


## Spring 의 구성 요소와 POJO
Spring은 다음과 같은 여러 기능을 통해 POJO 를 지원함.


* Dependency Injection(DI)
	Spring 의 DI 기능을 통해, 객체는 필요한 의존성을 외부에서 주입받을 수 있으므로, 각 객체는 의존성 구성에 대해 알 필요가 없음. 
	
	➡️ 코드의 결합도를 낮추고, 유연성과 테스트 용이성을 향상시킴.

* Aspect-Oriented Programming(AOP)
	AOP 를 사용하여 트랜잭션 관리나 보안과 같은 서비스를 POJO 에 적용할 수 있음.

* Transaction Management
	Spring 은 선언적 트랜잭션 관리를 제공하여 POJO 에 트랜잭션 관리 코드를 작성할 필요가 없도록 한다.

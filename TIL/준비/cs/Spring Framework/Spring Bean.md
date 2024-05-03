---
sticker: lucide//bean
---
* Index
	* Spring Bean 이란?
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
	스프링 빈을 사용하면 애플리케이션의 다양한 부분을 잘 정의된 컴포넌트로 나눌 수 있음. 각 컴포넌트는 스프링 빈으로 등록되어 서로 독립적으로 작동할 수 있으며, 필요한 의존성만 주입받아 사용함. ➡️ 코드의 결합도를 낮추고, 각 컴포넌트의 재사용성과 테스트 용
#spring 

## AOP 란?
* 관점 지행 프로그래밍
* 객체 지향 프로그래밍의 단점을 해소하기 위해 등장함.
	* Object Oriented Programming
	* 모든 변수 선언 시 new 를 통해 객체를 선언
	* 객체를 재사용 한다는 측면에서 효율적이었으나 공통된 부가기능에 대한 코드가 중복, 반복된다는 단점이 있음.

```java
public class Service{
	private void logMessage() {
		System.out.println("Action Performed");
	}

	public void processUserInput() {
		logMessage();
		// User input processing logic
		System.out.println("Processing user input ... ");
	}
	
	public void processData() {
		logMessage();
		// Data processing logic
		System.out.println("Processing data...");
	}
}
```

각 메소드에서 로깅을 수행하고 있음.  이 경우 로깅 방법을 변경하면 모든 메소드를 업데이트 해야함.

*  기존의 절차 지향 프로그래밍(POP) 이나 객체 지향 과는 다른 접근 방식을 제공
	* 주로 애플리케이션의 핵심 로직에서 분리해야 할 공통 기능(로깅, 보안, 트랜잭션 처리 등) 을 관리하는데 유용함.

```C
#include <stdio.h>
void logMessage() {
	printf("Action Performed\n");
}

void processUserInput() {
	logMessage();
	// User input processing logic
	printf("Processing user input ... \n");
}

void processData() {
	logmessage();
	// Data processing logic
	printf("Processing data...\n");
}

int main() {
	processUserInput();
	processData();
	return 0;
}
```

위 코드에서 `logMessage()` 함수는 각 기능 수행 전에 호출이 됨. 로깅 로직이 변경되면 모든 함수를 수정해야함.


### 관점 지행 프로그래밍 예시

AOP 를 사용하면 이러한 로깅 로직을 `Aspect` 로 분리하여 메소드의 실행 전후에 자동적으로 로깅을 수행할 수 있음. 아래는 예시임.

```java
import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.Before;
import org.aspectj.lang.annotation.After;

@Aspect
public class LoggingAspect {
    @Before("execution(* Service.*(..))") // Service 클래스의 모든 메소드 실행 전
    public void beforeAdvice() {
        System.out.println("Action Performed");
    }

    @After("execution(* Service.*(..))") // Service 클래스의 모든 메소드 실행 후
    public void afterAdvice() {
        System.out.println("Action completed");
    }
}
```

위 코드에서 `Service` 클래스의 모든 메소드가 실행되기 전과 후에 로깅이 자동으로 이루어짐.

로직이 중복되지 않으며, 로깅 방식을 변경하고 싶을 때는 `LoggingAspect` 클래스만 수정하면 됨.


### AOP 의 핵심
1. Aspect (관점)
	애플리케이션의 여러 부분에 걸쳐 영향을 미치는 모듈화된 관심사. 로깅이나 보안 검사는 여러 메소드나 클래스에 걸쳐 필요할 수 있음.

2. Advice(어드바이스)
	어떤 조인 포인트에서 실행되어야 할 코드임. 주로 before, after, around 의 형태로 구현이됨.
	* Before Advice : 조인 포인트 전에 실행됨.
	* After Advice : 조인 포인트가 성공적으로 완료된 후 실행됨.
	* Around Advice : 조인 포인트를 감싸서 조인 포인트의 실행 전후에 작업을 수행할 수 있음.

3. Pointcut(포인트 컷)
	어드바이스가 적용될 조인 포인트를 정의하는 표현식임. 특정 메소드 호출이나 필드 접근 등을 지정할 수 있음.

4. Join Point
	프로그램 실행 중 어드바이스가 적용될 수 있는 지점, 예를 들어서 메소드 호출이나 예외 발생 등임.





## 장점

* 모듈성 증가
	관심사를 분리하여 각각을 독립적으로 개발하고 유지보수 할 수 잇어 소프트웨어의 모듈성이 향상됨.

* 재사용성 향상
	같은 관점을 다른 프로젝트나 애플리케이션에서 쉽게 재사용할 수 있음.

* 가독성 및 유지보수성 향상
	핵심 로직에서 부가적 기능을 분리함으로써 코드의 가독성과 유지보수성이 개선됨.



## 단점

* 복잡성이 증가함.
	AOP는 애플리케이션의 구조를 더욱 추상화하고 관점을 분리하여 코드의 일부 동작을 감춤. 
	
	코드의 흐름을 직관적으로 이해하기 어렵게 만들 수 있으며, 특히 AOP 에 익숙하지 않은 개발자들에게는 실행 과정의 추적이 어렵게 할 수 있음.

* 디버깅 및 테스트의 어려움 
	어드바이스가 코드의 여러 부분에 적용되기 때문에 디버깅이 복잡해질 수 있음.
	
	특정 어드바이스의 영향을 받는 코드를 모두 파악하기 어려울 수 있으며, 에러가 발생했을 때 해당 에러가 핵심 로직에서 발생한 것인지 아니면 어떤 어드바이스에서 발생한 것인지 구분하기가 어려움.

* 성능 오버헤드
	AOP 구현은 일반적으로 런타임에 어드바이스를 적용하는 방식으로 이루어짐.
	이는 메소드 호출 시마다 관련 어드바이스를 확인하고 실행하는 추가적인 계산이 필요하므로 성능 저하를 일으킬 수 있음.
	
	특히 많은 수의 조인 포인트와 어드바이스가 있는 대규모 시스템에서는 이러한 오버헤드가 눈에 띄게 될 수 있음.

* 도구 및 플랫폼 의존성
	AOP 를 효과적으로 사용하기 위해서는 특정 프레임워크나 도구(Spring AOP, AspectJ) 에 대한 의존성이 발생함.
	
	이러한 도구들은 설정이 복잡할 수 있으며, 프로젝트의 기술 스택에 해당 도구들에 강하게 결속될 수 있음.

* 재사용성 문제
	AOP 를 사용하면 재사용성이 향상될 수 있지만, 어드바이스의 재사용성은 그 적용 가능성에 크게 의존함.
	
	특정 애플리케이션 또는 특정 유형의 문제에 맞춰진 어드바이스는 다른 컨텍스트나 다른 문제에는 적합하지 않을 수 있어, 재사용성이 제한적일 수 있음.

* 코드의 가독성
	모듈성을 향상시키는 장점이 존재하지만, 때로는 코드의 흐름을 파악하기 어렵게 만들 수 있음.
	
	코드 내에서 직접적으로는 보이지 않는 어드바이스 로직이 실행되기 때문에, 전체적인 로직을 이해하기 위해 AOP 구성을 꼼꼼하게 확인해야함.


### 어디서 사용됨?
* 로깅
	애플리케이션의 모든 서비스 메소드에 로그를 남기는 경우, 로깅 관점을 정의하여 필요한 모든 포인트컷에 자동으로 적용할 수 있음.

* 트랜잭션 관리
	데이터베이스 트랜잭션의 시작과 종료를 자동화하여 비즈니스 로직에서 분리할 수 있음.

* 보안
	메소드 실행 전 사용자의 인증 및 권한을 검사하는 보안 관점을 적용할 수 있음.


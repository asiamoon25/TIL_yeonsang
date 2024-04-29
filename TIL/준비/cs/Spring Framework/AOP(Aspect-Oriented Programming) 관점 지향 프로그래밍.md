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

AOP 를 사용하면 이러한 로깅 로직을 `Aspect` 로 분리하여 메소드의 실행 전후에 자동적으로 로깅을 수행할 수 있음.
#Java #keyword

## Static 이란

![[Pasted image 20240414113907.png]]

### static?
* 사전적 정의로는 정적인 의 뜻을 가지고 있음.
	* 사전적인 의미로만 봐도 불변한다는 걸 알 수 있음.. 막 건들면 에러날거 같은...
* JAVA 에서는 최초 클래스를 로드할때 메모리에 할당해 종료될 때 해제 되는 것을 의미.


### 메모리 할당?
[JVM](obsidian://open?vault=TIL_yeonsang&file=TIL%2F%EC%A4%80%EB%B9%84%2Fcs%2FJava%2FJVM)
위 글의 Runtime Data 영역을 보면 method area, heap area가 보이는데 method area 의 설명을 보면

클래스 정보를 처음 메모리에 올릴 때 초기화 되는 대상을 저장하기 위한 영역
	* 올라가는 정보
		1. Field Information
			* 멤버 변수에 대한 정보(이름,타입,접근 지정자 등)
		2. Method Information
			* 메서드에 대한 정보(이름, 리턴타입, 파라미터, 접근 지정자 등)
		3. Type Information

이렇게 설명이 되있는데 이때 static 변수가 method area 에 저장되고, GC 의 관리를 받지 않고 프로그램 종료 시 까지 유지된다.
> GC 의 대상은 Heap 영역이다.


### static keyword 특징
1. 클래스 레벨 공유
	static 변수는 클래스의 모든 인스턴스에 의해 공유됨. 이 변수들은 클래스가 메모리에 로드될 때 생성되고, 프로그램이 종료될 때까지 유지됨.

2. 메모리 효율
	같은 클래스의 모든 객체들이 하나의 `static` 변수를 공유하기 때문에 메모리 사용이 줄어듬.

3. 인스턴스 없이 접근 가능
	static 메서드나 변수는 객체의 인스턴스를 생성하지 않고도 호출할 수 있음. 클래스 이름을 통해 직접 접근 가능.
	이미 method area에 있으므로 객체가 생성되기 전에 할당되어 있기 때문이다.
```java
public class MyClass {
	public static String staticValue = "HI";
	public static int staticMethod(int a, int b) {
		return a + b;
	}
}


public class TestClass {
	public static void main(String args[]) {
		String a = MyClass.staticValue;
		int resultA = MyClass.staticMethod(1,2);
		  
		MyClass m1 = new MyClass();
		
		int resultB = m1.staticMethod(1, 2);
	}
}
```


### 좋은데 왜 다 static 안함?

**객체 지향 설계 위반**
* **캡슐화 저하**
	`static` 변수는 클래스의 모든 인스턴스에 의해 공유됨. 이는 데이터 캡슐화를 저하시켜, 객체 간의 상호 작용을 예측하기 어렵게 만들 수 있음. 
	객체 지향의 핵심은 각 객체가 독립적인 상태와 행동을 갖는건데 `static` 많이 쓰면 이 원칙이 박살남.

 * **의존성 문제**
	 `static` 메서드는 인스턴스 변수나 메서드에 접근할 수 없음. 
	 이로 인해 `static` 메서드가 많아지면, 클라스의 다른 비 `static` 부분과의 결합도가 낮아져, 객체 지향적 설계가 어려워짐.


**테스트와 유지보수의 어려움이 있음**

* **테스트의 어려움** 
	`static` 변수나 메서드는 테스트가 어려움. `static` 변수는 애플리케이션의 생명주기 동안 초기화 되거나 변경된 값이 유지되기 때문에, 테스트 간 상태를 초기화 하기 어려워짐. ▶️ 격리된 테스트 환경을 만드는데 어려움을 가짐.

* **유지보수 복잡성**
	`static` 메서드나 변수가 많은 시스템은 시간이 지남에 따라 관리하기가 더 복잡해짐. 
	`static` 요소들은 시스템의 다른 부분과 강하게 결합될 수 있고, 이로 인해 코드의 변경이 필요할 때 예상치 못한 부작용을 발생시킬 수 있음.


**메모리 관리**
* **메모리 사용증가**
	`static` 변수는 프로그램이 종료 될 때 까지 메모리에 남아 있음. 따라서, 많은 양의 데이터를 `static` 으로 관리하면서 메모리 사용량이 증가하고, 필요하지 않은 데이터도 계속 메모리를 차지하게 됨. ▶️ 장시간 실행되는 애플리케이션에서 문제가 될 수 있음.


**동시성 문제**
* **스레드 안전 문제**
	멀티스레드 환경에서 `static` 변수에 여러 스레드가 동시에 접근하게 되면 동시성 문제가 발생할 수 잇음. ▶️ 데이터의 일관성과 정확성을 보장하기 어렵게 만들며, 추가적인 동기화 처리가 필요하게 됨.


### 그럼 언제씀?

#### 1. 공유된 상수
* 여러 인스턴스에서 공통적으로 사용되는 상수 값은 `static final` 로 선언하여 사용함.
```java
public class MathConstants {
	public static final double PI = 3.14159;
}
```

#### 2. 유틸리티 메서드
* 객체의 상태에 의존하지 않는 메서드, 즉 입력 값만으로 결과를 반환하는 순수 함수는 `static` 메서드로 선언이 됨.
```java
public class StringUtils {
	public static boolean isEmpty(String s) {
		return s == null || s.isEmpty();
	}
}
```
#### 3. 싱글턴 패턴
_최근에 DB Connection Pool 을 start up 되는 시점부터 잡아서 DB 점검일 때 DB 연결이 안되면 어플리케이션 전체가 실행 안되는 상황이 있었는데 기존  프레임워크에서 제공해주는 DataSource 를 지우고, Custom DataSource 를 만들어서 해결했는데 이렇게 싱글턴 패턴으로 만들어서 해결했음._
```java
public class Singletom{
	private static Singleton instance;
	privatet Singleton() {}

}
```

#### 4. 클래스 초기화 블록

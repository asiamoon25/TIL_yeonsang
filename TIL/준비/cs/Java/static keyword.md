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

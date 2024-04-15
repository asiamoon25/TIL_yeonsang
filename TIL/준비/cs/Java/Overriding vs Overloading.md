#Java 


## Overriding 과 super

* 부모 클래스로부터 상속받은 메서드의 내용을 재정의(변경) 하는 것


### 조건
* 오버라이딩은 메서드를 새로 만드는게 아니고 내용만 새로 작성하는 것
* 알맹이만 변경한다.

1. 메소드 시그니처 일치
	오버라이딩하는 메소드는 슈퍼 클래스에서 선언된 메소드와 동일한 이름, 매개변수 목록 및 반환 유형을 가져야함. 메소드 시그니처가 일치해야만 실제로 메소드가 오버라이딩 되는 것으로 간주함.

2. 접근 제한자
	오바리이딩 하는 메소드는 원본 메소드보다 더 제한적인 접근 제한자를 가질 수 없음
	ex) 슈퍼 클래스의 메소드가 `protected` 로 선언되었다면, 서브 클래스의 메소드는 `protected` 또는 `public` 이여야함.

3. 반환타입
	자바 5 이상에서는 오버라이딩된 메소드의 반환 타입이 원본 메소드의 반환 타입의 서브타입일 수 있음.(공변 반환 타입)
	ex) 슈퍼 클래스의 메소드가 `Number` 타입을 반환한다면, 서브 클래스 메소드는 `Integer` 와 같은 `Number` 의 서브 클래스를 반환할 수 있음.

4. 예외
	오버라이딩하는 메소드는 원본 메소드가 선언한 예외보다 더 일반적인 예외를 던질 수 없음. 또한 체크된 예외를 던지는 경우, 오버라이딩하는 메소드가 던질 수 있는 예외는 원본 메소드가 던질 수 있는 예외들의 서브 타입이거나 동일한 예외여야함.
	ex) 슈퍼 클래스의 메소드가 `NullPointer` 를 던진다면, 오버라이딩하는 메소드는 `NullPointer` 또는 `NullPointer` 의 하위 Exception 을 던질 수 있음.
	서브 클래스의 메소드가 `RuntimeException` 을 던지면 안됨.

5. `static` 메소드는 오버라이딩 불가
	정적 메소드는 오버라이딩 되지 않음. 서브 클래스에서 같은 시그니처의 정적 메소드를 선언하면, 이는 메소드 숨김(Hiding) 현상이 발생함.

6. `final` 메소드는 오버라이딩 불가
	`final` 로 선언된 메소드는 오버라이딩 할 수 없음. 이러한 메소드는 변경을 허용하지 않는 최종적인 구현을 가짐.

7. 스레드 안전과 동기화
	오버라이딩하는 메소드가 원본 메소드가 스레드 안전인지 또는 동기화되어 있는지에 따라, 서브 클래스에서도 동일한 특성을 유지해야할 수도 있음.
	필수적인 규칙은 아니지만 프로그램의 일관성과 안정성을 위해 고려해야함.


### super
스-파

`super` 는 자식 클래스에서 부모 클래스의 멤버(변수,메소드) 에 접근하거나, 부모 클래스의 생성자를 호출할 때 사용됨.

**주요 사용방법**

1. 부모 클래스의 생성자 호출
	`super()` 는 자식 클래스의 생성자에서 사용되며, 부모 클래스의 생성자를 호출함. 이 호출은 자식 클래스의 생성자 내에서 가장 먼저 이루어져야 함. 부모 클래스에 매개변수가 필요한 생성자만 있는 경우, `super` 를 사용하여 필요한 값들을 전달해야함.
```java
public class Parent {
	public Parent(String name) {
		System.out.println("Parent Constructor: "+name);
	}
}
...

public class Child extends Parent {
	public Child() {
		super("Hello"); // 부모 클래스 생성자 호출
		System.out.println("Child Constructor");
	}
}
```

2. 부모 클래스의 메소드 호출
	자식 클래스에서는 `super` 키워드를 사용하여 부모 클래스에서 정의된 메소드에 접근할 수 있음. 특히 메소드 오버라이딩 상황에서 유용하며, 오버라이딩 된 메소드에서 원본 메소드의 기능을 확장하거나 재사용할 때 사용됨.
```java
public class Parent {
	public void display() {
		System.out.println("Parent display()");
	}
}

public class Child extends Parent{
	public void display() {
		super.display();
		System.out.println("Child display()");
	}
}
```


3. 부모 클래스의 필드 접근
	자식 클래스에서 `super` 를 사용하여 부모 클래스의 필드(멤버 변수)에 접근할 수 있음. ▶️ 변수 이름이 중복될 때 유용함.
```java
public class Parent {
	protected int number = 100;
}
...

public class Child extends Parent {
	private int number = 200;

	public void showNumber() {
		System.out.println(super.number);
		System.out.println(this.number);
	}
}
```


---

## Overloading
![[Pasted image 20240415154319.png]]

### Overloading 이란?
* 한 클래스 내에 같은 이름의 메서드를 여러 개 정의하는 것


### 조건

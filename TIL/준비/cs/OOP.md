## OOP 란?

* Object-Oriented Programming
* C언어 같이 절차지향적이 아니라 객체 지향적으로 프로그램한다는 뜻
* 객체를 기준으로 코드를 나누어 구현

## 특징

### 캡슐화(Encapsulation)

* 하나의 객체에 대해 그 객체가 특정한 목적을 위한 필요한 변수나 메소드를 하나로 묶는 것을 의미

* 정보 은닉
	캡슐화를 하는 중요한 목적은 정보은닉에 있다. public 으로 된 객체에 접근해서 정보 변경이 가능하여 private 로 해서 접근을 제한해야함.
	getter, setter 로 정보 접근해야함.

==캡슐화와 정보 은닉은 동일 개념이 아님. 캡슐화를 하면 정보를 감출 수 있기 때문에 정보은닉이 가능하다는 특징이 있다는 것==


### 추상화(Abstraction)
* 목적과 관련이 없는 부분을 제거하여 필요한 부분만을 표현하기 위한 개념

공통적인 요소나 특징을 추출하는 과정이라고 생각하면됨.

추상 메서드는 구현부가 없으므로 {} 대신 끝을 표시해주는 의미로 ; 을 적어줌.
하위 클래스로 상속하여 실행할 수 있는데, 이때 사용하게 되는 것이 @Override 이다. 이것으로 메서드를 완성시키고, 이렇게 완성된 클래스로 해당 인스턴스를 생성할 수 있음.

```java
abstract class Dog {
	abstract void sleep(); // 추상 메서드
	abstract void bark(); // 추상 메서드
}
...
class Poodle extends Dog {
	void sleep() {
		Thread.sleep(5000); // 추상 메서드 구현 
	}
}
...
abstract class Pome extends Dog {
	void bark() {
		System.out.println("wal wal");
	}
}
```



## 다형성(Polymorphism)

* 형태가 같은데 다른 기능을 하는 것을 의미(같은 동작이지만 다른 결과물이 나올 때 다형이라고 생각하면됨.)
* 이를 통해 코드의 재사용, 코드 길이 감소가 되어 유지보수가 용이하도록 도와줌.

### Override & Overloading

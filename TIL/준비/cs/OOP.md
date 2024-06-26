---
sticker: lucide//package-2
---
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

- 오버라이딩  
    - 부모 클래스에서 상속받은 자식 클래스에서 부모클래스에서 만들어진 메서드를 자식 클래스에서 재정의해서 사용하는 것
- 오버로딩  
    - 이름은 같지만 파라미터가 다름...

### 좋음?

같은 이름의 속성을 유지함으로서, 속성을 사용하기 위한 인터페이스를 유지하고, 메서드 이름을 낭비하지 않는다는 것
API 가 많아질수록 복잡성은 증가하기 때문에 다형성은 유용하다.


## 상속성, 재사용(Inheritance)

* 상속이란 기존 상위 클래스에 근거하여 새롭게 클래스와 행위를 정의할 수 있게 도와주는 개념
* 기존 클래스에 기능을 가져와 재사용할 수 있으면섣 동시에 새롭게 만든 클래스에 새로운 기능을 추가할 수 있게 만들어줌.
==_자바는 인터페이스에서만 다중 상속되고 나머지는 단일 상속임ㅋㅋ_==

### 왜 필요?

* 코드의 중복을 없애기 위함.


---

_코드 재사용 용이라면 인터페이스랑 추상클래스랑 같은거 아님? 뭔차이?_

* 인터페이스
	1) 모든 메서드가 기본적으로 추상 메서드이고 java 8 이후부터는 default 메서드와 static 메서드를 통해 구현 코드를 포함할 수 있게 됨.
	2) 필드는 오직 public static final(상수)만을 가질 수 있음.
	3) 하나의 클래스가 여러 인터페이스를 구현할 수 있음.
	4) 서로 다른 클래스들이 같은 인터페이스를 구현함으로써, 다형성을 제공하는데 사용
* 추상클래스
	1) 하나 이상의 추상 메서드를 포함할 수 있음, 구현된 메서드도 포함할 수 있음.
	2) 필드에 대한 제한이 없음. 상수 뿐만 아니라 상태(멤버변수)를 가질 수 있음.
	3) 단 하나의 추상 클래스만을 상속(extend) 할 수 있으며, 이는 다중 상속의 제한을 의미함.
	4) 관련 있는 클래스들 사이에서 코드를 공유하거나, 특정 메서드의 구현을 강제하기 위해 사용됨. 

#### 요약 

* **추상화 수준** : 인터페이스는 보다 높은 수준의 추상화를 제공. "할 수 있는" 것들에 초점이라면, 추상클래스는 "하는 방법" 에 대한 일부 구현을 포함
	==Flyable, Drawable== 같이 행동을 정하지만 그 행동이 어떻게 수행되어야 하는 하는지에 대해서는 명시하지 않음. 추상 메소드만 있기 때문..
	
* **다중상속** : 인터페이스를 사용하면 다중 상속이 가능하지만, 추상 클래스를 상속하는 경우 단일 상속만 가능.
* **구성 요소** : 인터페이스는 주로 추상메서드로 구성되지만, java8 이후로는 일부 구현된 메서드를 가질 수 있음. 추상 클래스는 추상 메서드 뿐만 아니라 구현된 메서드와 멤버 변수도 가질 수 있음.
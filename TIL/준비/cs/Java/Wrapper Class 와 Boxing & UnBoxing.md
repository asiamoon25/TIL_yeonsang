---
sticker: lucide//codesandbox
---
## Wrapper
JAVA 에서는 기본 타입을 객체로 다루기 위해 Wrapper 클래스를 제공함.

`int` -> `Integer`
`double` -> `Double`
...

Wrapper 클래스는 해당 기본 타입의 값을 가지고 있고, 객체로 다양한 기능을 수행할 수 있음.

래퍼 클래스를 이용하면 각 타입에 해당하는 데이터를 파라미터로 전달받아 해당 값을 가지는 객체로 만들어준다.
```java
Integer num1 = new Integer(5);
Integer num1 = 5;
// 이렇게 2개로 표현 가능

Double num2 = new Double(1.11);
Double num2 = 1.11;
```

---

## Boxing & UnBoxing


### Boxing
* 기본 타입을 Wrapper 클래스 객체로 변환하는 과정
* `int` -> `Integer` 로 변환하는 과정임.


### UnBoxing
* Wrapper Class 객체를 기본 타입 값으로 변환하는 과정을 말함.
* `Integer` -> `int` 로 변환하는 과정임.

```java
// Boxing
Integer num = new Integer(20); // Integer Wrapper Class num2 에 21 의 값을 저장

//UnBoxing
int n = num.intValue(); // Wrapper Class num 의 값을 꺼내 가져옴.

//재 포장
n = n  + 100;
num = new Integer(n);
```


---

## AutoBoxing & AutoUnBoxing

## ?
* JAVA 5 부터 도입된 기능으로, 기본 타입 값을 Wrapper 클래스 객체로 자동으로 변환해주는 기능.
* 코드를 간결하게 만들어주고 가독성을 높여줌

```java
//Boxing
Integer num = new Integer(10); // int 를 Integer객체로 Boxing

// UnBoxing
int value = num.intValue(); // Integer 객체를 int 로 UnBoxing

//AutoBoxing
Integer num2 = 20; // int 를 Integer 로 오토박싱
```

근데 이거 잘못하면 박살날 수 있음


```java
Integer a = null;
int b = 50;
System.out.println(a + b);

-> NullPointException
```

### Wrapper Class Compare

Auto UnBoxing 을 통해 객체 값을 더하고 빼는건 문제가 없지만 비교할때는 조심.

객체의 주소값 == 값   이렇게 연산할 수 있어서 의도하지 않은 동작이 일어남.

```java
Integer num1 = new Integer(100);
Integer num2 = new Integer(100);

num1 == num2; // -> false 나옴
```

**그러면?**

직접 언박싱해서 비교하거나 아니면 `equals()` 메소드를 통해 비교 가능
```java
Integer num1 = new Integer(10);
Integer num2 = new Integer(20);
Integer num3 = new Integer(30);

System.out.println(num1 == num3); // false
System.out.println(num1.equals(num3)); // true

// == 외에 문제는 없음
System.out.println(num1 < num2); // true
System.out.println(num1 + num2); // 30
```

**Wrapper Class 와 기본 자료형은 ㄱㅊ**
```java
Integer num1 = new Integer(5);
int i = 5; 

System.out.println(num == i);    //  true

System.out.println(num.equals(i)); // true
```
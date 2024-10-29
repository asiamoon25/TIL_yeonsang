#Java #keyword 

## final keyword 란

Java 에서 final keyword 는 유저(사용자) 를 제한한다.
final keyword 는 많은 부분에서 사용되는데 final keyword 는 아래에서 사용된다.
1. 변수
2. 메소드
3. 클래스

final keyword 는 변수와 함께 적용될 수 있는데, 값이 없는 final 변수를 공백 final 변수 또는 초기화 되지 않은 final 변수 라고 한다.

이때 생성자에서만 초기화 할 수 있다.

```java
public class FinalKeyWord {  
	final String uninitializedValue;  
	  
	FinalKeyWord(){  
		this.uninitializedValue = "Hello World";  
	}  
}
...
public class FinalKeyWordTest() {
	FinalKeyWord fkw = new FinalKeyWord();
	System.out.println(fkw.uninitializedValue);
}
...

➡️ Hello Wolrd
```

또한 공백 final 변수는 정적 블록에서만 초기화되는 정적 변수일 수도 있음. ⬇️자세하게 보도록 하자.


### 1. Java final Variable
임이의 변수를 final 로 만들면 final variable 의 값을 변경할 수 없음. (상수가 됨.)

**ex)**
```java
public class Bike9{
	final int speedLimit = 90;   // final variable
	
	void run() {
		speedLimit = 400;
	}
	public static void main(String args[]) {
		Bike9 obj = new Bike9();
		obj.run();
	}
}
➡️ Output:Compile Time Error
```


### 2. Java final method
메소드를 final 로 만들면 이를 재정의 할 수 없음 (@Override...)

**ex)**
```java
public class Bike{
	final void run() {System.out.println("running");}
}

public class Honda extends Bike{
	void run(){System.out.println("running safely with 100kmph");}
	
	public static void main(String args[]) {
		Honda honda = new Honda();
		honda.run();
	}
}
➡️ Output : Compile Time Error
```

### 3. Java final Class

대충 상속 못함...
```java
final class Bike{}

class Honda1 extends Bike{
	void run() {System.out.println("running safely with 100kmph");}
	
	public	static void main(String args[]) {
		Honda1 honda = new Honda1();
		honda.run();
	}
}
➡️ Output:Compile Time Error
```

#### 그러면 final method 는 상속됨?
ㅇㅇ 됨.
```java
public class Bike{
	final void run() {System.out.println("running...");}
}
class Honda2 extends Bike{
	public static void main(String args[]) {
		new Honda2().run();
	}
}
➡️ Output: running...
```


#### 그러면 static final 도 공백 final 변수이면 초기화 가능?

ㅇㅇ 가능함. 대신에 static 안에서 초기화 해야함.

```java
class A {
	static final int data; // static blank final variable
	static{data = 50;}
	public static void main(String args[]) {
		System.out.println(A.data);
	}
}
```

#### final parameter 라는 것도 있는데...

파라미터를 final 로 하면, 변경할 수 없음...

```java
class Bike11{
	int cute(final int n) {
		n = n + 2; // n 이 final 이므로 변경이 안된다.
		n *= n;
	}
	public static void main (String args[]) {
		Bike11 b = new Bike11();
		b.cube(5);
	}
}
➡️ Compile Error
```


#### 생성자 final 로 만들 수 있음? 
?







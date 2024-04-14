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
public class MyClass {
	final String uninitializedValue;
	
	MyClass(){
		this.uninitializedValue = "Hello World";
	}
}
```
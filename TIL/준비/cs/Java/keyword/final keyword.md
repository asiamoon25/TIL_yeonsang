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
```

```

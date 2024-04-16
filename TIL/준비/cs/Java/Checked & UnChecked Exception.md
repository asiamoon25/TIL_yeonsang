
## Checked and Unchecked Exception

* JAVa 에서 예외 처리 메커니즘은 크게 두 가지 유형의 예외로 나눌 수 있음.
* Checked Excetpion
* Unchecked Exception



## Checked Exception

* RuntimeException 의 하위 클래스가 아니면서 Exception 클래스의 하위 클래스들임.
* 체크 예외의 특징은 반드시 에러 처리를 해야하는 특징(try/catch or throw) 을 가지고 있음.
	FileNotFoundException
	ClassNotFoundException
	이런 것들이 있음.


## Unchecked Exception

* RuntimeException 의 하위 클래스
* Checked Exception 과는 달리 에러 처리를 강제하지 않음. Runtime 중에 발생할 수 있는 예외를 의미함.
	ArrayIndexOutOfBoundsException
	NullPointerException

### 왜 강제하지 않음?

1. 프로그래밍의 오류를 나타내기 때문
	Unchecked Exception 은 대부분 프로그래머의 실수로 인해 발생함.
	이러한 오류들은 일반적으로 실행 중이 아닌, 코드를 작성하는 단계에서 수정되어야 함.
	즉, 이런 종류의 오류들은 런타임에 정상적으로 회복될 수 있는 예외적인 상황이 아니라, 프로그램의 버그로 간주되기 때문에, 강제적인 예외처리르로는 적절하지 않을 수 있음.

2. 코드의 간결성 유지
	모든 예외를 강제로 체크하도록 하면 코드가 매우 길어지고 복잡해짐.
	예외 처리를 강제하는 것은 코드를 읽기 어렵게 만들고, 실제 중요한 로직에 집중하기보다는 오류 처리에 많은 코드를 쓰는 상황을 초래할 수 있음.
	Unchecked Exception 을 사용함으로써 개발자는 필요에 따라 예외를 처리할 수 있으며, 코드의 가독성과 유지 관리성을 향상 시킬 수 있음.

3. 유연성 제공
	프로그래머가 런타임 오류를 예상하고 적절히 대응할 수 있는 경우에는 Unchecked Exception 을 사용하여 보다 유연하게 예외처리를 할 수 있음.
	
	ex) 개발자는 특정 메소드에서 `NullPointerException` 이 발생할 가능성이 있다는 것을 알고 있을 수 있으나, 이를 명시적으로 처리하기보다는 해당 객체가 절대 `null` 이 아니도록 보장함으로써 더 깔끔하고 효율적인 코드를 작성할 수 있음.

```java
public class UncheckedExceptionExample {
	public static void main(String[] args) {
		try{
			int result = divide(10,0); // 이 줄에서 ArithmeticException 발생
			System.out.println("Result : " + result);
		}
	}
}
```


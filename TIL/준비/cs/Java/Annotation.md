#Java #Annotation

## Annotation 이란

* 사전적 의미로의 주석
	* 일반적인 주석 // 나 /\*\*/ 와는 다름.
	* 코드를 작성할 수 있음.
	* ⭐프로그램의 소스코드 안에 다른 프로그램을 위한 정보를 미리 약속된 형식으로 포함시킨 것
* 다른 프로그램에게 유용한 정보를 제공하기 위해 사용되는 것으로 주석과 같은 의미를 가짐.
* **역할**
	* 컴파일러에게 문법 에러를 체크하도록 정보를 제공함.
	* 프로그램을 빌드할 때 코드를 자동으로 생성할 수 있도록 정보를 제공함.
	* 런타임에 특정 기능을 실행하도록 정보를 제공함.

## 특징

* 주석이기 때문에 다이나믹하게 실행되는 코드는 들어가지 않음.
	* 런타임 중에 알아내야하는 값은 못들어감
	* 컴파일러 수준에서 해석되거나, 완전히 정적이여야함.


## 주요 용도
1. **컴파일러에 대한 지시사항**
	어노테이션을 사용하여 컴파일러에게 경고를 억제하거나 오류를 체크하도록 지시할 수 있음. 
		ex) `@Deprecated` ➡️ 메소드나 클래스가 더 이상 사용되지 않으며 대체될 것이라는 것을 나타냄.
2. **코드 분석**
	소프트웨어 개발 도구가 코드 구조를 분석하거나 코드에 더 많은 정보를 제공할 때 사용됨.
3. **런타임 처리**
	어노테이션은 런타임에 리플렉션을 통해 조회될 수 있어, 동적으로 코드의 행동을 변경하는 데 사용될 수 있음. 
		ex) `@Autowired` ➡️ 스프링 프레임워크에서 의존성 주입을 자동으로 처리하는 데 사용됨.
4. **프레임워크 및 API 개발**
	자바 프레임워크와 라이브러리는 사용자가 클래스나 메소드에 어노테이션을 적용함으로써 필요한 설정을 간편하게 할 수 있도록 지원함. 
		ex) REST API 상에서 `@GetMapping` 과 `@PostMapping` 은 HTTP GET 과 POST 요청을 처리하기 위해 사용됨.


_아니 특징에는 동적 실행 코드는 안들어간다고 해놓고 용도에는 동적으로 코드의 행동을 변경하는데 사용 될 수 있다고 하는데 구라 아님?_
![[Pasted image 20240412232449.png]]

### ⚠️ 구라가 아님.
```
구라가 아닌 이유는 위 두 내용에 나온 "동적" 이라는 의미를 구분하는게 중요함.
어노테이션이 직접적으로 코드의 실행을 동적으로 변화 시키지는 않지만, 어노테이션 정보를 활용하여 런타임 시 코드의 동작을 변경할 수 있는 메커니즘을 제공함.
```
두 가지 설명이 있는데
1. **어노테이션 자체는 실행되지 않는다**
	
	어노테이션 자체는 코드의 일부로 실행되지 않는다. 
	
	즉, 어노테이션이 "실행" 되어 어떤 코드를 직접 변경하거나 조작하지는 않음. 
	
	주석처럼 메타데이터를 제공하는 역할을 하면서 이 메타 데이터는 컴파일 시간이나 런타임 때 다른 메커니즘에 의해 해석되어 사용됨.

2. **런타임 시 어노테이션을 기반으로 동작을 변경**
	
	여러 프레임워크와 라이브러리는 리플렉션 API 를 사용하여 런타임에 어노테이션의 정보를 읽고, 그 정보에 따라 특정 동작을 수행할 수 있도록 한다. 
	
	예를들어, 스프링 프레임워크에서 `@Transactional` 어노테이션이 메소드에 적용되면, 스프링은 해당 메소드의 실행을 트랜잭션 관리 로직으로 감싸 동적으로 트랜잭션을 관리함.
	
	 ➡️ 어노테이션이 "동적" 으로 코드 실행을 하는게 아니라, 어노테이션을 해석하여 해당 로직을 적용하는 프레임워크의 동작 덕분에 가능한 일임.

```java
@RestController
public TestController() {
	private static final String value = "Value";

	@GetMapping(value)
	public String v() {
		return "value";
	}
}
```
value 가 static final 한 정적변수이기 때문에 @GetMapping 어노테이션에 사용해도 문제가 안됨. 근데 value 가 `private String value = "value";` 라면 어노테이션에 사용하지 못함. Compile Error 발생함.




## 정의하는 방법

`@interface <어노테이션 이름>`

```java
public @interface MyAnnotation{
	// type 요소 이름();
}
```
@interface는 어노테이션 타입을 선언하는 키워드
인터페이스 정의 방식과 비슷함.

### 어노테이션 필드

* 필드의 타입은 기본형, `String` , `enum`, Annotation, Class 만 가질 수 있음.
* () 안에 매개변수를 선언할 수 없음.
* 예외를 선언할 수 없음
* 요소를 타입 매개변수로 정의할 수 없음
* 배열은 선언할 수 있음. String[] arr();
* default 값을 지정할 수 있음. null 제외 모든 리터럴 가능

```java
@interface ExAnnotation {
	int number() default 100; // int type (기본형)
	String value(); // String
	String[] arr(); // array
	Month month(); // Enum Type
	Class exClass(); // class
	Target tg(); // Tartget Annotation
}
```
어노테이션의 요소는 return 값이 있고 매개변수는 없는 추상 메서드의 형태를 가짐.
⬇️

```java
@ExAnnotation(
	value = "java",
	arr = {"hello", "world"},
	month = Month.FEB,
	exClass = MyClass.class
	tg = @Target(ElementType.ANNOTATION_TYPE)
)
public void Class {
	...
}
```


----


## JAVA 표준 어노테이션

1. @Override
	* 선언한 메서드가 오버라이드 됬다는 것을 나타냄.
	* 만약 부모 클래스(또는 인터페이스) 에서 해당 메서드를 찾을 수 없다면 컴파일 에러를 발생시킴

2. @Deprecated
	* 해당 메서드가 더 이상 사용되지 않음을 표시함.
	* 만약 사용할 경우 컴파일 경고를 발생시킴.

3. @SuppressWarnings
	* 선언한 곳의 컴파일 경고를 무시 하도록 함.

4. @SafeVarargs
	* JAVA 7 부터 지원, 제너릭 같은 가변 인자의 매개변수를 사용할 때의 경고를 무시

5. @FunctionalInterface
	* JAVA 8 부터 지원하며, 함수형 인터페이스를 지정하는 어노테이션
	* 만약 메서드가 존재하지 않거나, 1개 이상의 메서드(default method 제외) 가 존재할 경우 컴파일 오류를 발생시킴.


## 메타 어노테이션 (기타 어노테이션에 적용되는 어노테이션)

1. @Retention
	* 자바 컴파일러가 어노테이션을 다루는 방법을 기술하며, 특정 시점까지 영향을 미치는지를 결정함.
	* **종류**
		* RetentionPolicy.SOURCE : 컴파일 전까지만 유효(컴파일 이후 사라짐)
		* RetentionPolicy.CLASS : 컴파일러가 클래스를 참조할 때까지 유효.
		* RetentionPolicy.RUNTIME : 컴파일 이후에도 JVM에 의해 계속 참조가능(리플렉션 사용)

2. @Documented
	* 해당 어노테이션을 Javadoc 에 포함시킴 

3. @Target
	* 어노테이션이 적용할 위치를 선택
	* **종류**
		- **ElementType.PACKAGE** : 패키지 선언
		- **ElementType.TYPE** : 타입 선언
		- **ElementType.ANNOTATION_TYPE** : 어노테이션 타입 선언
		- **ElementType.CONSTRUCTOR** : 생성자 선언
		- **ElementType.FIELD** : 멤버 변수 선언
		- **ElementType.LOCAL_VARIABLE** : 지역 변수 선언
		- **ElementType.METHOD** : 메서드 선언
		- **ElementType.PARAMETER** : 전달인자 선언
		- **ElementType.TYPE_PARAMETER** : 전달인자 타입 선언
		- **ElementType.TYPE_USE** : 타입 선언

4. @Inherited
	* 어노테이션의 상속을 가능하게 함.

5. @Repeatable
	* JAVA 8 부터 지원하며, 연속적으로 어노테이션을 선언할 수 있게 해줌.



---

https://techblog.woowahan.com/2684/
우아한 기술블로그에 있는 어노테이션..
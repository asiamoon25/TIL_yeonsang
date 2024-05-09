
Spring 에서 Controller 로 들어오는 입력값에 대한 유효성 검증을 위해서 Java Bean Validation API 와 Spring Validator 를 사용할 수 있음.




## Java Bean Validation
* 어노테이션 기반으로 간단하게 검증할 수 있음.

1. 의존성 추가
	`pom.xml` 또는 `build.gradle` 에 의존성을 추가함.

**Maven(`pom.xml`)
```xml
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-validation</articatId>
</dependency>
```

**Gradle(`build.gradle`)**

```gradle
implementation 'org.springframework.boot:spring-boot-starter-validation'
```


2. DTO 작성
	검증이 필요한 입력 데이터에 어노테이션을 활용하여 유효성 검증을 설정함.
```java
public class UserRequest {
	@NotBlank(message = "Name is required")
	private String name;

	@Min(value = 18, message = "Age should not be less than 18")
	@Max(value = 100, message = "Age should not be greater than 100")
	private int age;
	
	@Email(message = "Invalid email format")
	private String email;
	
	//Getter/Setter
	public
}
```
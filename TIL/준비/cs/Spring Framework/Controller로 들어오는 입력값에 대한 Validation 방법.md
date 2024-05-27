
Spring 에서 Controller 로 들어오는 입력값에 대한 유효성 검증을 위해서 Java Bean Validation API 와 Spring Validator 를 사용할 수 있음.




## Java Bean Validation
* 어노테이션 기반으로 간단하게 검증할 수 있음.

1. 의존성 추가
	`pom.xml` 또는 `build.gradle` 에 의존성을 추가함.

**Maven(`pom.xml`)**
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
	public String getName() {
		return name;
	}
	
	public void setName(String name) {
		this.name = name;
	}
	
	public int getAge() {
		return age;
	}
	
	public void setAge(int age) {
		this.age = age;
	}
	
	public String getEmail() {
		return email;
	}
	
	public void setEmail(String email) {
		this.email = email;
	}
}
```

3. Controller 에서 유효성 검증 적용
	Controller 메서드에 `@Valid` 와 `BindingResult` 를 사용하여 검증 결과를 처리함.
```java
@RestController
@RequestMapping("/users")
public class UserController {

	@PostMapping
	public String createUser(@RequestBody @Valid UserRequest userRequest, BindingRequest result){
		if(result.hassErrors()) {
			return result.getFieldErrors().stream()
			.map(fieldError -> fieldError.getField() + ":" + fieldError.getDefaultMessage())
			.reduce((message1, message2) -> message1 + ", "+message2)
			.orElse("Invalid input");
		}
		return "User created successfully!";
	}

}
```


## Spring Validator Interface

1. Custom Validator 구현
```java
@Component
public class UserRequestValidator implements Validator{
	@Override
	public boolean supports(Class<?> clazz) {
		return UserRequest.class.euquals(clazz);
	}
	
	@Override
	public void validate(Object target, Errros errors) {
		UserRequest userRequest = (UserRequest) target;
		
		if(userRequest.getName() == null || userRequest.getName().isBlank()) {
			errors.rejectValue("name", "name.required", "Name is required");
		}
		
		if(userRequest.getAge() < 18 || userRequest.getAge() > 100){
		errors.rejectValue("age", "age.invalid", "Age should be between 18 and 100");
		}
		
		if(userRequest.getEmail() == null || !userRequest.getEmail().contains("@")){
			errors.rejectValue("email","email.invalid", "Invalid email format");
		}
	}
}
```

2. Controller 에서 사용
```java
@RestController
@RequestMapping("/users")
public class UserController {

    @Autowired
    private UserRequestValidator userRequestValidator;

    @InitBinder
    protected void initBinder(WebDataBinder binder) {
        binder.setValidator(userRequestValidator);
    }

    @PostMapping
    public String createUser(@RequestBody UserRequest userRequest, BindingResult result) {
        userRequestValidator.validate(userRequest, result);

        if (result.hasErrors()) {
            return result.getFieldErrors().stream()
                .map(fieldError -> fieldError.getField() + ": " + fieldError.getDefaultMessage())
                .reduce((message1, message2) -> message1 + ", " + message2)
                .orElse("Invalid input");
        }
        return "User created successfully!";
    }
}
```
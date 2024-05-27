#spring 

## Spring Container 란?

* 스프링 프레임워크의 핵심 컴포넌트
* 자바 객체의 생명 주기를 관리하며, 생성된 자바 객체들에게 추가적인 기능을 제공함.
	* 스프링에서는 자바 객체를 Bean 이라고 함.
	* 생성, 구성, 조립 및 관리하는 역할을 함.


### 주요기능
1. 빈 생명주기 관리
	Bean 의 생성부터 소멸까지의 전체 생명주기를 관리함.
	빈의 생성, 의존성 주입, 초기화 후 처리, 그리고 소멸 시의 처리를 포함.

2. 의존성 주입
	클래스 간의 의존성을 외부에서 주입해 줌으로써 느슨한 결합을 유지할 수 있게 도와줌.
	클래스가 자신이 필요로 하는 의존 객체를 직접 생성하지 않고, 외부에서 제공 받을 수 있게 함으로써 코드의 재사용성과 유지보수성을 향상시킴.

3. 빈 설정과 관리
	컨테이너는 XML 파일, 어노테이션, 자바 설정 클래스 등을 통해 빈을 구성할 수 있음.
	이 설정들을 통해 빈의 프로퍼티를 설정하거나 초기화 메소드를 호출하는 등의 작업을 수행함.



## 유형

### BeanFactory

* 빈을 관리하고 의존성을 주입하는 가장 간단한 컨테이너. 주로 리소스가 제한된 장치에서 사용됨.

#### **예제**

**HelloWorld.java**
```java
publc class HelloWorld {
	private String message;
	
	public void setMessage(String message) {
		this.message = message;
	}
	
	public void getMessage() {
		Syste.out.println("Your Message : " + message);
	}
}
```


**beans.xml**
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="helloWorld" class="HelloWorld">
        <property name="message" value="Hello Spring!"/>
    </bean>
</beans>
```

**Main.java**
```java
import org.springframework.beans.factory.BeanFactory;
import org.springframework.beans.factory.xml.XmlBeanFactory;
import org.springframework.core.io.ClassPathResource;

public class Main {
    public static void main(String[] args) {
        BeanFactory factory = new XmlBeanFactory(new ClassPathResource("beans.xml"));
        HelloWorld helloWorld = (HelloWorld) factory.getBean("helloWorld");
        helloWorld.getMessage();
    }
}
```


### ApplicationContext

* BeanFactory 를 확장한 컨테이너로, 메시지 자원 처리, 이벤트 발행 및 다양한 더 풍부한 기능을 제공함. 일반적인 스프링 애플리케이션에서는 ApplicationContext 가 사용됨.

#### 예제

**HelloWorld.java**
```java
public class HelloWorld {
	private String message;
	
	public void setMessage(String message) {
		this.message = message;
	}
	
	public void getMessage() {
		System.out.println("Your Message : " + message);
	}
}
```

**AppConfig.java**

```java
@Configuration
public class AppConfig {
	@Bean
	public HelloWorld() {
		HelloWorld helloWorld = new HelloWorld();
		helloWorld.setMessage("Hello Spring!");
		return hellWorld;
	}
}
```


**Main.java**

```java
import org.springframework.context.ApplicationContext;
import org.springframework.context.annotation.AnnotationConfigApplicationContext;

public class Main {
    public static void main(String[] args) {
        ApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);
        HelloWorld helloWorld = context.getBean(HelloWorld.class);
        helloWorld.getMessage();
    }
}
```


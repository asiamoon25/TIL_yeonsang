
## Interceptor 란

* 가로채다
* 요청/응답 또는 메서드 실행을 가로채고 그 전후로 추가적인 처리를 수행하는 컴포넌트임.
* 사용자의 요청이 컨트롤러에 가기 전에 가로채고, 서버의 응답이 사용자에게 가기 전에 가로챔. HttpRequest, HttpResponse 객체를 가로채어 가공함.

### Spring MVC HandlerInterceptor(Spring Framework)
* 역할 : Spring MVC 의 컨트롤러에 대한 요청을 가로채 전처리 또는 후처리 로직을 수행함.
* 메서드
	* `preHandle()` : 컨트롤러가 실행되기전에 호출
	* `postHandle()` : 컨트롤러가 실행된 후에 호출되지만, 뷰를 렌더링하기 전
	* `afterCompletion()` : 뷰 렌더링까지 완료된 후에 호출됨.

#### **예시**
```java
import org.springframework.web.servlet.HandlerInterceptor;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

public class LoggingInterceptor implements HandlerInterceptor {
    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        System.out.println("Request URI: " + request.getRequestURI());
        return true; // true를 반환하면 다음 인터셉터 또는 컨트롤러로 요청을 계속 전달
    }

    @Override
    public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) throws Exception {
        System.out.println("PostHandle: After handling the request");
    }

    @Override
    public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {
        System.out.println("AfterCompletion: After completing the request and response");
    }
}
```

**Interceptor 등록**
```java
import org.springframework.context.annotation.Configuration;
import org.springframework.web.servlet.config.annotation.InterceptorRegistry;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurer;

@Configuration
public class WebConfig implements WebMvcConfigurer {
    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        registry.addInterceptor(new LoggingInterceptor())
                .addPathPatterns("/**") // 모든 경로에 대해 적용
                .excludePathPatterns("/exclude"); // 제외할 경로
    }
}
```

#### **JPA/Hibernate Interceptor**

* 엔티티가 변경되기 전후로 동작하며, 데이터베이스 조작에 대한 추가 로직을 수행함.
```java
import org.hibernate.EmptyInterceptor;
import org.hibernate.type.Type;
import java.io.Serializable;

public class EntityInterceptor extends EmptyInterceptor {
    @Override
    public boolean onSave(Object entity, Serializable id, Object[] state, String[] propertyNames, Type[] types) {
        System.out.println("Saving entity: " + entity);
        return false; // 상태 변경 시 true 반환
    }

    @Override
    public void onDelete(Object entity, Serializable id, Object[] state, String[] propertyNames, Type[] types) {
        System.out.println("Deleting entity: " + entity);
    }

    @Override
    public boolean onFlushDirty(Object entity, Serializable id, Object[] currentState, Object[] previousState, String[] propertyNames, Type[] types) {
        System.out.println("Updating entity: " + entity);
        return false;
    }
}
```

**추가**
```java
import org.hibernate.SessionFactory;
import org.hibernate.cfg.Configuration;

public class HibernateUtil {
    private static final SessionFactory sessionFactory;

    static {
        try {
            sessionFactory = new Configuration()
                    .setInterceptor(new EntityInterceptor()) // 인터셉터 등록
                    .configure()
                    .buildSessionFactory();
        } catch (Throwable ex) {
            throw new ExceptionInInitializerError(ex);
        }
    }

    public static SessionFactory getSessionFactory() {
        return sessionFactory;
    }
}
```

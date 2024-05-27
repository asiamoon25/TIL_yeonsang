## Filter 란?

* Http 요청 및 응답을 가로채어 전처리 및 후처리 로직을 수행하는 데 사용되는 서블릿 기반의 컴포넌트
* 주로 인증, 인가, 로깅, 데이터 압축 등의 기능을 제공함.
* web.xml 에 등록하고, 인코딩 변환 처리, XSS 방어 등의 요청에 대한 처리로 사용됨.

Servlet 필터는 DispatcherServlet 이전에 실행이 되는데 필터가 동작하도록 지정된 자원의 앞단에서 요청내용을 변경하거나, 여러가지 체크를 수행할 수 있음.


### 특징
* `javax.servlet.Filter` 인터페이스를 구현함.
* 서블릿 컨테이너에서 관리되며, 모든 HTTP 요청 및 응답에 대해 전역적으로 작동함.
* filter 는 순차적으로 적용됨. 
* Spring Security 등의 인증/인가 프레임워크에서도 핵심 컴포넌트로 활용됨.

**주요 메서드**
* `init(FilterConfig filterConfig)` : 필터 초기화 시 호출됨.
* `doFilter(ServletRequest request, ServletResponse response, FilterChain chain)` : 실제 필터링 로직이 수행됨.
	* `chian.doFilter(request,response)` : 다음 필터 또는 최종 목적지(servlet/controller) 로 요청을 전달함.
	* `destroy()` : 필터 인스턴스가 컨테이너에서 제거될 때 호출됨.


### 예시

#### log filter
```java
import javax.servlet.*;
import javax.servlet.http.HttpServletRequest;
import java.io.IOException;

public class LoggingFilter implements Filter {
    @Override
    public void init(FilterConfig filterConfig) throws ServletException {
        // 필터 초기화 로직
        System.out.println("Initializing LoggingFilter");
    }

    @Override
    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
        HttpServletRequest httpRequest = (HttpServletRequest) request;
        System.out.println("Request URI: " + httpRequest.getRequestURI());
        
        // 다음 필터 또는 서블릿으로 요청을 계속 전달
        chain.doFilter(request, response);
        
        System.out.println("Response Status: " + response.getContentType());
    }

    @Override
    public void destroy() {
        // 필터 소멸 시 정리 로직
        System.out.println("Destroying LoggingFilter");
    }
}
```

**filter 등록**
1. web.xml
```xml
<filter>
    <filter-name>loggingFilter</filter-name>
    <filter-class>com.example.LoggingFilter</filter-class>
</filter>
<filter-mapping>
    <filter-name>loggingFilter</filter-name>
    <url-pattern>/*</url-pattern>
</filter-mapping>
```

2. Java Config
```java
import org.springframework.boot.web.servlet.FilterRegistrationBean;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class FilterConfig {
    @Bean
    public FilterRegistrationBean<LoggingFilter> loggingFilter() {
        FilterRegistrationBean<LoggingFilter> registrationBean = new FilterRegistrationBean<>();
        registrationBean.setFilter(new LoggingFilter());
        registrationBean.addUrlPatterns("/*");
        registrationBean.setOrder(1); // 필터 실행 순서 지정
        return registrationBean;
    }
}
```

3. `@WebFilter` 어노테이션
```java
import javax.servlet.*;
import javax.servlet.annotation.WebFilter;
import java.io.IOException;

@WebFilter(urlPatterns = "/*")
public class AnnotationLoggingFilter implements Filter {
    @Override
    public void init(FilterConfig filterConfig) throws ServletException {
        System.out.println("Initializing AnnotationLoggingFilter");
    }

    @Override
    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
        System.out.println("Filtering request in AnnotationLoggingFilter");
        chain.doFilter(request, response);
    }

    @Override
    public void destroy() {
        System.out.println("Destroying AnnotationLoggingFilter");
    }
}
```

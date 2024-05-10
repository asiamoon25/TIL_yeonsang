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

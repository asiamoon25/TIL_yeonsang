
## Interceptor 란

* 가로채다
* 요청/응답 또는 메서드 실행을 가로채고 그 전후로 추가적인 처리를 수행하는 컴포넌트임.
* 사용자의 요청이 컨트롤러에 가기 전에 가로채고, 서버의 응답이 사용자에게 가기 전에 가로챔. HttpRequest, HttpResponse 객체를 가로채어 가공함.

### Spring MVC HandlerInterce
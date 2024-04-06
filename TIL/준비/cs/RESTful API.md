---
sticker: lucide//download
---
### REST API
* Representational State Transfer 라는 용어의 약자

### REST 구성
* 자원(RESOURCE) - URI
* 행위(Verb) - HTTP METHOD
* 표현(Representations)

### REST 의 특징

1) Uniform (유니폼 인터페이스)
	Uniform Interface 는 URI 로 지정한 리소스에 대한 조작을 통일되고 한정적인 인터페이스로 수행하는 아키텍처 스타일
	
2) Stateless (무상태성)
	REST 는 무상태성 성격을 가짐. 작업을 위한 상태정보를 따로 저장하고 관리하지 않음. 세션 정보나 쿠키 정보를 별도로 저장하고 관리하지 않기 때문에 API 서버는 들어오는 요청만을 단순히 처리하면 됨. ➡️ 서비스의 자유도가 높아지고 서버에서 불필요한 정보를 관리하지 않음으로써 구현이 단순해짐.
	
3) Cacheable (캐시 가능)
	REST 의 가장 큰 특징 중 하나는 HTTP 라는 기존 웹표준을 그대로 사용하기 때문에 웹에서 사용하는 기존 인프라를 그대로 활용이 가능함. 따라서 HTTP 가 가진 캐싱 기능이 적용 가능함. HTTP 프로토콜 표준에서 사용하는 Last-Modified 태그나 E-Tag 를 이용하면 캐싱 구현이 가능함.
	
4) Self-descriptiveness (자체 표현 구조)
	REST 의 또 다른 큰 특징 중 하나는 REST API 메시지만 보고도 이를 쉽게 이해할 수 있는 자체 표현 구조로 되있음.
	
5) Client - Server 구조
	REST 서버는 API 제공, 클라이언트는 사용자 인증이나 컨텍스트(session, 로그인 정보) 등을 직접 관리하는 구조로 각각의 역할이 확실히 구분되기 때문에 클라이언트와 서버에서 개발해야 할 내용이 명확해지고 서로간의 의존성이 줄어들게 됨.
	
6) 계층형 구조
	REST 서버는 다중 계층으로 구성될 수 있으며 보안,로드 밸런싱, 암호화 계층을 추가해 구조상의 유연성을 둘 수 있고 PROXY, Gate way 같은 네트워크 기반의 중간매체를 사용할 수 있게 함.


### REST API 디자인 가이드

1. URI 는 정보의 자원을 표현해야 한다.
2. 자원에 대한 행위는 HTTP Method(GET, POST, PUT, DELETE)로 표현한다.

1) REST API 중심 규칙
	* URI 는 정보의 자원을 표현해야 한다.(리소스명은 동사보다는 명사를 사용)
		`GET /members/delete/1`
		위와 같은 방식은 REST를 제대로 적용하지 않은 URI. URI 는 자원을 표현하는데 중점을 둬야함. delete 와 같은 행위에 대한 표현이 들어가서는 안됨.
		
	* 자원에 대한 행위는 HTTP Method(GET, POST, PUT, DELETE 등)로 표현
		위 잘못된 부분을 수정하면
		`DELETE /members/1` 이렇게 됨.
		회원정보를 가져올 때는 GET, 회원 추가 시의 행위를 표현하고자 할때는 POST 를 사용하여 표현
		
		**회원정보를 가져오는 URI**
		`GET /members/show/1 (X)`
		`GET /members/1 (O)` 
		
		**회원을 추가할 때**
		`GET /members/insert/2 (X)` -> GET 메서드는 리소스 생성에 맞지 않음.
		`GET /members/2 (O)`

| METHOD | 역할                                                         |
| ------ | ---------------------------------------------------------- |
| POST   | POST를 통해 해당 URI를 요청하면 리소스를 생성합니다.                          |
| GET    | GET를 통해 해당 리소스를 조회합니다. 리소스를 조회하고 해당 도큐먼트에 대한 자세한 정보를 가져온다. |
| PUT    | PUT를 통해 해당 리소스를 수정합니다.                                     |
| DELETE | DELETE를 통해 리소스를 삭제합니다.                                     |
2) URI 설계 시 주의할 점
	1. 슬래시 구분자는 계층 관계를 나타내는 데 사용
		`http://restapi.example.com/houses/apartments`
		`http://restapi.example.com/animals/mammals/whales`

	2. URI 마지막 문자로 슬래시(/) 를 포함하지 않는다.
	   
		URI 에 포함되는 모든 글자는 리소스의 유일한 식별자로 사용되어야 하며 URI 가 다르다는 것은 리소스가 다르다는 것이고, 역으로 리소스가 다르면 URI 도 달라져야함. 
		
		REST API 는 분명한 URI 를 만들어 통신을 해야하기 때문에 혼동을 주지 않도록 URI 경로의 마지막에는 슬래시(/) 사용하지 않음.
		
		`http://restapi.example.com/houses/apartments/ (X)`
		`http://restapi.example.com/houses/apartments (O)`

	3. 하이픈(-) 은 URI 가독성을 높이는데 사용
		
		URI 를 쉽게 읽고 해석하기 위해, 불가피하게 긴 URI 경로를 사용하게 된다면 하이픈을 사용해 가독성을 높일 수 있음.

	4. 밑줄(\_)은 URI 에 사용하지 않는다.
	   
		글꼴에 따라 다르긴 하지만 밑줄은 보기 어렵거나 밑줄 때문에 문자가 가려지기도함. 
		\_ 보다는 - 을 사용하는게 좋다.
	   
	   
	5. URI 경로에는 소문자가 적합하다.
		
		대소문자에 따라 다른 리소스로 인식하기 쉬움. 
		
		RFC3986(URI 문법 형식)은 URI 스키마와 호스트를 제외하고는 대소문자를 구별하도록 규정함.
		`RFC 3986 is the URI (Unified Resource Identifier) Syntax document`
		
	6. 파일 확장자는 URI 에 포함시키지 않는다.
	   
		`http://restapi.example.com/members/soccer/photo.jpg (X)`
		
		Accept header 를 사용
		`GET /members/soccer/photo HTTP/1.1 Host: restapi.example.com Accept: image/jpg`

3)  리소스 간의 관계를 표현하는 방법
	REST 리소스 간에는 연관 관계가 있을 수 있고, 이런 경우 다음과 같은 표현방법으로 사용
	`/리소스명/리소스 ID/관계가 있는 다른 리소스명`
	`ex) GET : /users/{userid}/devices (일반적으로 소유 'has'의 관계를 표현할 때`
	
	관계명이 복잡하면 서브 리소스에 명시적으로 표현
	`GET : /users/{userid}/likes/devices (관계명이 애매하거나 구체적 표현이 필요할 때)`

4) 자원을 표현하는 Collection 과 Document
	이것을 알면 URI 설계가 더 쉬워짐.
	Document 는 문서로 이해해도 되고, 한 객체라고 이해해도 됨. 
	
	Collection 은 문서들의 집합, 객체들의 집합 이라고 생각하면 됨. 
	
	Collection 과 Document 는 모두 리소스라고 표현할 수 있으며 URI에 표현됨.
	`http://restapi.example.com/sports/soccer`
	
	sports 라는 컬렉션과 soccer라는 도큐먼트로 표현되고 있다고 생각하면 됨.
	`http://restapi.example.com/sports/soccer/players/13`
	
	sports, players Collection 과 soccer,13(13번인 선수)를 의미하는 Document 로 URI 가 이루어지게 됨. 
	여기서 보여지는 것은 Collection 이 복수로 사용되고 있다는 점.. s 를 붙이자

### HTTP 응답 상태 코드
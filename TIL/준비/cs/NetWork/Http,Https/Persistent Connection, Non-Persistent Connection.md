## 1. Persistent Connection

### 정의

* 지속적인 연결은 클라이언트와 서버 간의 TCP 연결을 여러 HTTP 요청과 응답에 걸쳐 유지하는 방식
* HTTP/1.1 에서는 기본적으로 지속적인 연결이 설정되어 있으며, `Connection: keep-alive` 헤더를 통해 명시적으로 지속 연결을 요청할 수 있음.


### 장점
* 연결 및 종료에 소요되는 시간과 자원을 절약할 수 있음.
* 네트워크 지연을 감소시키고, 전체적인 통신 성능을 향상시킴.
* 여러 자원(이미지,css 파일, 자바스크립트 등)을 빠르게 로드할 수 있음.

### 사용

* 웹 페이지에서 다수의 리소스를 빠르게 로드해야 할 때 유리함.
* 네트워크 지연이 성능에 큰 영향을 미치는 환경에서 효과적임.


**예시**
HTTP/1.1 응답에서 Persistent Connection의 사용
```yaml
HTTP/1.1 200 OK
Date: Mon, 23 May 2022 12:00:00 GMT
Server: Apache/2.4.1 (Unix)
Content-Type: text/html
Content-Length: 1234
Connection: keep-alive
Keep-Alive: timeout=10, max=50
```


## 2. Non-Persistent Connection(비지속적인 연결)

### 정의
* 각 HTTP 요청마다 새로운 TCP 연결을 생성하고 요청/응답이 끝나면 즉시 연결을 종료하는 방식
* HTTP/1.0 의 기본 연결 방식, 각 요청이 독립적으로 처리됨.

### 장점
* 서버에 지속적인 연결로 인한 부하가 적음
* 서버 리소스 관리가 단순해지며, 각 요청이 완전히 독립적으로 처리됨.

### 단점
* 연결 및 종료를 반복해야 하므로 추가적인 시간과 자원이 소모됨.
* 네트워크 지연과 로드 시간이 증가할 수 있음.

### 사용
* 간단한 요청이나 서버 부하를 최소화해야 할 때 사용됨.
* 서버와의 연결을 짧게 유지해야 하는 보안상의 이유로 사용될 수 있음.

**예시**
HTTP/1.0 요청에서 비지속적인 연결의 사용
```yaml
HTTP/1.0 200 OK
Date: Mon, 23 May 2022 12:00:00 GMT
Server: Apache/2.4.1 (Unix)
Content-Type: text/html
Content-Length: 1234
Connection: close
```

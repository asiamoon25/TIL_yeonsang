
## 란?

* Persistent Connection 을 설정하고 유지하는 데 중요한 역할을 하는 녀석
* HTTP/1.1 에서는 모든 연결이 기본적으로 Persistent Connection 으로 처리되지만 `keep-alive header` 를 통해 이 연결들을 더 세밀하게 제어할 수 있음.


## 역할

`keep-alive header` 는 HTTP/1.0 에서 중요한 역할을 함.
HTTP/1.0 은 기본적으로 비지속적인 연결을 사용하므로, `keep-alive header` 를 통해 클라이언트와 서버가 연결을 유지하기를 원한다는 것을 명시해야함. 이 header 는 다음과 같은 정보를 포함할 수 있음.

* `timeout` : 연결이 유휴 상태로 유지될 최대 시간(초 단위)
* `max` : 연결을 통해 전송될 수 있는 최대 요청 수

## HTTP/1.1 에서의 Keep-Alive

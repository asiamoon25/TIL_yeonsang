
## 란?

* Persistent Connection 을 설정하고 유지하는 데 중요한 역할을 하는 녀석
* HTTP/1.1 에서는 모든 연결이 기본적으로 Persistent Connection 으로 처리되지만 `keep-alive header` 를 통해 이 연결들을 더 세밀하게 제어할 수 있음.


## 역할

`keep-alive header` 는 HTTP/1.0 에서 중요한 역할을 함.
HTTP/1.0 은 기본적으로 비지속적인 연결을 사용하므로, `keep-alive header` 를 통해 클라이언트와 서버가 연결을 유지하기를 원한다는 것을 명시해야함. 이 header 는 다음과 같은 정보를 포함할 수 있음.

* `timeout` : 연결이 유휴 상태로 유지될 최대 시간(초 단위)
* `max` : 연결을 통해 전송될 수 있는 최대 요청 수

## HTTP/1.1 에서의 Keep-Alive

HTTP/1.1 에서는 `Connection: keep-alive` 를 명시적으로 선언할 필요는 없지만, 연결의 파라미터를 조정하거나, 특히 서버가 HTTP/1.0 클라이언트를 지원해야 할 때 이 헤더를 사용함.

**request 예시**
```makefile
GET /image.png HTTP/1.1
Host: example.com
Connection: keep-alive
Keep-Alive: timeout=5, max=100
```

이 요청에서 클라이언트는 서버에 `image.png` 파일을 요청하여, 연결을 5초 동안 유지하고 최대 100개의 요청을 처리할 수 있도록 요청함.

**response 예시**
```makefile
HTTP/1.1 200 OK
Date: Wed, 21 Oct 2020 07:28:00 GMT
Server: Apache/2.4.1 (Unix)
Last-Modified: Wed, 21 Oct 2020 07:12:00 GMT
Content-Type: image/png
Content-Length: 2048
Connection: keep-alive
Keep-Alive: timeout=5, max=99
```

이 응답에서 서버는 클라이언트에게 요청한 이미지를 보내면서 `keep-alive` 헤더를 통해 연결을 추가적으로 5초 동안 유지하며, 이전에 1개의 요청을 처리했으므로 남은 최대 요청 수를 99로 설정함.

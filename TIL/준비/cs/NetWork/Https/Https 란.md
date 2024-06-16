### 개념

* HTTPS 는 HyperText Transfer Protocol Secure 의 약자
* 웹 통신 프로토콜인 HTTP의 보안 버전
* 데이터의 안전한 전송을 위해 사용됨.
* 데이터가 전송되는 도중 도청, 중간자 공격, 데이터 변조 등을 방지함.



### HTTPS 랑 HTTP 의 차이는?

1. **보안성**
	* HTTP : 데이터를 암호화하지 않고 평문으로 전송하기 때문에 도청 및 데이터 변조에 취약함.
	* HTTPS : SSL/TLS 를 사용하여 데이터를 암호화하여 전송하므로 데이터의 기밀성과 무결성을 보장함.

2. **포트번호**
	* HTTP : 기본적으로 80 포트 사용함.
	* HTTPS : 기본적으로 443 포트를 사용함.

3. **인증서**
	* HTTP : `http://` 로 시작함.
	* HTTPS : `https://` 로 시작함.


### S 가 Secure 인거 아는데 어캐함?

* SSL(Secure Sockets Layer) 또는 TLS(Transport Layer Security) 프로토콜에 기반함.
* SSL 은 더 이상 사용되지 않으며, 현대의 HTTPS 는 모두 TLS 를 사용함.


 1. 대칭 키 암호화(Symmetric Key Encryption)

	* 개념 : 동일한 키를 사용하여 데이터를 암호화하고 복호화 하는 방식
	* 장점 : 암호화와 복호화가 빠르고 효율적임.
	* 단점 : 키의 분배와 관리가 어려움.
	* 알고리즘 예시 : AES(Advanced Encryption Standard), DES(Data Encryption Standard)


2. 
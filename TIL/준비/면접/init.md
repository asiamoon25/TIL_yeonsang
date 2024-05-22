JAVA BE 면접 질문 정리

# JAVA

1. JVM 에 대해서, GC의 원리
2. GC 의 종류
3. GC 선택 가이드원리
4. JAVA 메모리 영역
5. Collection
6. TreeSet, TreeMap ↔️ HashSet, HashMap
7. Array vs ArrayList & LinkedList
8. Annotation
9. Generic
10. static keyword
11. final keyword
12. Overriding vs Overloading
13. Access Modifier
14. Wrapper class Boxing 과 Unboxing, AutoBoxing
15. Checked & UnChecked Exception
16. Multi-Thread 환경에서의 개발
17. == 연산자, equals(), hashCode
18. Interface vs Abstract Class, Abstract method
19. 리플렉션이란?
20. Java Class 멤버 변수 초기화 순서
21. Java 버전별 특징 - 어느 버전에서 어떤 기능이 추가되었는지
22. OOP의 3대 조건과 5대 원칙
23. 좋은 객체 지향 프로그램이란

# Spring

1. Spring FrameWork의 핵심
	1. POJO 기반의 구성
	2. 제어의 역전(IoC)
	3. 의존성 주입
		1. DI 와 IoC
		2. DI 와 DIP
		3. 스프링에서의 의존성 주입이란
		4. 스프링에서는 어떻게 구현하는가?
		5. 왜 의존성 주입을 사용해야 하는가?
	4. DI 방식의 장단점
		1. 생성자(constructor) 주입
		2. 수정자(setter) 주입
		3. field 주입
	5. AOP(Aspect-Oriented Programming) 관점 지향 프로그래밍
	6. AOP 의 용어
	7. Spring Bean 이란?
	8. Spring Bean Scope
	9. Spring Bean LifeCycle
		1. Bean LifeCycle
		2. Bean LifeCycle CallBack
	10. Spring Container
	11. DL(Dependency LookUp) 이란?
2. SpringBoot 와 Spring 의 차이 (왜 Boot 를 쓸까?)
3. Controller로 들어오는 입력값에 대한 Validation 방법
4. Interceptor vs AOP vs Filter

---
실제 멘토님이 받은 면접 질문

# JAVA

1. GC 에 대해 설명
2. Interface 와 Abstract Class 차이
3. LinkedList 와 Abstract Class 의 차이
4. LinkedList 와 Array 차이
5. static keyword 란?
6. final keyword 란?
7. Overloading & Overriding
8. JAVA 에서 multi thread 구현 어떻게 하는지 & 장점
9. Java 11 특징
10. Boxing & UnBoxing
11. 리스코프 치환 원칙이란?

# Spring

1. SpringBoot 의 @Application Annotation 의 역할
2. DI - Spring 에서는 어떻게 구현하는지
3. Bean Scope
	1. Singletom
	2. Prototype
	3. Web
4. Bean LifeCycle
5. AOP

# DB

1. index 를 어떤 key에 설정하는지?
2. MySQL 에서 성능 확인을 위한 명령어
	* Explain
		* 실행 시 결과 값 중 어떤 값을 잘 봐야하는지?

3. NoSQL
	* MongoDB
# NetWork

1. HTTP Header
	* keep-alive header 란?
		* 왜 / 어떨 때 사용하는지?
	* TCP vs UDP
		* 3 ways handshake 란?
		* UDP 를 어떨때 사용?
	* OSI 7계층과 각 계층의 구성요소

# OS

* Process vs Thread
* DeadLock 이란?
* Non-Blocking 이란?

# Design Pattern

* 팩토리 패턴
* MSA
* EDA (Event Driven Architecture)

---

이 이후에도 공부할 것들...

# Programming Language
* JAVA
* Python
* JavaScript

# Version Control
* Git
* GitHub

# Internet
* HTTP
	* RESTful API
* DNS

# DB
* RDB
	* MySQL,MariaDB
* NoSQL
	* MongoDB

* DB 기본 지시 
	* ORM
	* ACID
	* N+1 문제

# 인증 관련
* 인증
* 인가
* OAuth

# OS 관련
* 터미널 사용방법

# FrontEnd 기본 지식 
* css
* HTML
* jQuery

# 배포 관련
1. CI
	1. GitHub Action
	2. Jenkins
2. CD
	1. 아르고 CD
	2. Docker
3. Container
	1. Docker
4. k8s

# Cloud Service
1. Azure

# 보안 관련
1. https
2. cors
3. owasp

# Web Framework
1. express
2. NestJS
3. Spring

# Message broker
1. RabbitMQ
2. Kafka

# 검색 엔진
1. elasticsearch

# 개발 방법론
1. DDD
2. TDD

# TEST
1. Unit Test
2. 통합 테스트

# Cache
1. Local Cache
2. 분산 캐시
	1. Redis
	2. memcached
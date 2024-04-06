---
sticker: emoji//1f3ea
---
#JavaCollectionFramework #List

**Vector**
* JDK 1.0 부터 있었던 자료 구조, 호환성을 위해 남겨 놓은 레거시 클래스
* Vector는 ArrayList와 기능상 거의 동일하지만, 다른점이 있음
	ArrayList는 비동기 방식, Vector 는 동기 방식
	
	**멀티쓰레드 환경에서는 Vectors를 써야함?**
	* 동기방식 : 요청을 보낸 후, 응답을 받아야 다음 과정이 동작하는 방식
	* 비동기 방식 : 요청을 보낸 후, 응답과는 상관 없이 다음 과정이 동작하는 방식
	* Thread Safe : 멀티 쓰레드 환경에서 어떤 함수나 변수, 혹은 객체가 여러 쓰레드로 부터 동시에 접근이 이루어져도 프로그램의 실행에 문제가 없음을 뜻함.
	* 비동기 방식 : Thread Safe 하지 않다.
	* 동기방식 : Thread Safe 하다.
	  
	ArrayList 는 Collections.synchronizedList() 를 사용해서 동기 방식의 리스트를 만들 수 있음.
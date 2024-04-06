---
sticker: emoji//1f929
---

#JavaCollectionFramework #List
* Vector 를 상속하여 사용하는 LIFO(Last In First Out) 방식의 클래스
* Java 에서는 Stack 대신 Deque 를 사용하여 구현할 것을 권장함.
	Stack 클래스를 까고 들어가보면
	![[Pasted image 20240405134349.png]]
	마지막 줄을 보면 Stack 이 처음 생성되면 항목이 포함되지 않는다고 나와 있음.
	`보다 완전하고 일관된 LIFO 스택 작업은 Deque 인터페이스와 그 구현에 의해 제공되며, 이 클래스 보다 먼저 사용해야 한다.`
	라고 나와 있음.
	
	* 쓰레드 안전성 및 동기화 오버헤드
		* Stack 은 Vector 를 상속하기 때문에 Vector 를 까고 들어가보면
		  ![[Pasted image 20240405134750.png]]
		  synchronized 를 자주 쓰는 것을 볼 수 있다. 멀티쓰레드 환경에서 데이터의 안정성을 보장하기 위해서 필요하지만 성능저하가 발생함.
		  하지만 ArrayDeque 는 동기화 메커니즘을 사용하지 않아 동기화에 따른 오버헤드가 발생하지 않음.
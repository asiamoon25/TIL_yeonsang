---
sticker: emoji//1f3f8
---
**Queue**
* FIFO 구조를 가진 자료구조
* 주로 LinkedList 를 이용하여 구현할 수 있음.
* Queue를 상속받은 구현체로 Deque 와 PriorityQueue 가 있음.

	1. Priority Queue
		Queue 인터페이스의 상속을 받으며 FIFO 가 아닌, 특정 우선순위에 다라 요소가 먼저 나가는 방식
		우선순위는 Comparator 를 통해 정의해주거나, Comparable 인터페이스를 상속한 객체를 이용해야함.
	2. Deque
		Interface
		Double-Ended Queue 의 약어로, Queue 의 양쪽 끝에서 추가와 삭제가 일어날 수 있는 자료구조.
		사용 방식에 따라 Stack 이 될 수도 Queue 가 될 수도 있음.
		Dequeue 의 구현체로 ArrayDeque 와 LinkedList 가 있음.
		
		* **ArraayDeque**
			* 사이즈 제한이 없는 가변 배열
			* null 요소는 저장할 수 없음
			* 비동기 방식
			* 원형 큐 방식으로 구현
			* Stack 목적으로 구현하였을때 기존의 Stack 보다 빠르고, Queue 목적으로 구현하였을 때 LinkedList 보다 빠름.
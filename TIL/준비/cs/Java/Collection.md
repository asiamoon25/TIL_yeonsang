---
sticker: emoji//2623-fe0f
---
# Java Collections Framework(JCF)

* Java Collections Framework 의 약어
* 다수의 데이터를 쉽고 효과적으로 처리할 수 있는 표준화된 방법을 제공하는 클래스의 집합
* 데이터를 저장하는 자료구조와 데이터를 처리하는 알고리즘을 구조화 하여 클래스로 구현
* Collection => 데이터의 집합이나 그룹

## 왜 씀?

**JCF 도입 전**

* Array, Vectors, Hashtable 이 있었으며, 공통인터페이스가 존재하지 않았음.
* 각 Collection 마다 사용하는 메소드, 문법, 생성자가 달랐기 때문에 혼동하기 쉬웠음.

```java
...
Vector<Integer> v = new Vector();
Hashtable<Integer, String> h = new Hashtable();

v.addElement();
h.put(1,"");
```

이래서 사용

**장점**
1) 코드 재사용이 쉬움
2) 데이터 구조 및 알고리즘의 고성능 구현을 제공하여 프로그램의 성능과 품질 향상
3) 관련없는 API 간의 상호 운용성을 제공
4) 새로운 API 를 익히고 설계하는 시간이 줄어듬
5) 소프트웨어 재사용을 촉진함. JCF 를 사용하는 새로운 데이터 구조가 재사용 가능하기 때문이며, 같은 이유로 JCF 를 사용하는 객체를 활용하여 새로운 알고리즘을 만들어낼 수 있음.


## 계층 구조

크게 Iterable 을 상속한 인터페이스와 Map 을 상속한 인터페이스로 나눌 수 있음.

* Iterable 을 포함한 인터페이스
	* List
	* Queue
	* Set
![[Pasted image 20240403145904.png]]

* Map 을 포함한 인터페이스
	* HashTable
	* LinkedHashMap
	* HashMap
	* TreeMap
![[Pasted image 20240403145921.png]]

### List

* 순서가 있는 데이터의 집합으로 데이터의 중복을 허용
* List 인터페이스 구현 클래스는 ArrayList, LinkedList, Vector, Stack이 있음.

**ArrayList**
* 크기가 가변적인 선형 리스트, 저장용량이 존재함.
	저장용량을 넘어서면 자동으로 증가시킴. default 는 10
	용량 증가 시 기존 용량 + 기존용량/2 만큼 증가시킴

**LinkedList**
* 각 노드가 데이터와 포인터를 가지고 한 줄로 연결되어 있는 자료 구조
	데이터를 담고 있는 노드들이 연결되어 있고, 노드의 포인터가 이전 노드와 다음 노드와의 연결을 담당
* 노드만 연결하면 되기 때문에 저장 용량이 존재하지 않음

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


**Stack**

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

**Set**
* 중복된 요소를 저장하지 않고, 요소의 저장 순서를 유지하지 않는 특징을 가짐.
* Set 의 구현체로 HashSet, LinkedHashSet, TreeSet 이 있음.
	**중복된 요소 걸러내는 법**
	* equals() 와 hashCode() 를 사용
		1. 객체를 저장하기 전에 해시 코드를 호출해서 해시코드를 얻어냄.
		2. Set 에 저장되어 있는 요소들의 해시코드와 비교
		3. 만약 같은 해시코드가 있다면 equals() 메소드로 두 객체를 비교
		4. equals() 메소드가 true 가 나오면 중복으로 판단하여 저장하지 않음.

**HashSet**

* Set 을 이용하기 위해 가장 많이 사용하는 구현 클래스
* HashSet 은 해시 알고리즘을 사용하여 검색속도가 빠르다는 장점이 있음.
	* HashSet 의 인스턴스는 HashMap 의 인스턴스를 통해 생성

**LinkedHashSet**
* HashSet 과 원리는 같으나, 입력된 순서를 저장한다는 특징이 있음.
* HashSet 의 상속을 받으며, LinkedHashMap 을 통해 구현되어 있음.

**TreeSet**
* 특정 기준에 따라 요소를 정렬할 수 있게 해줌
	* 생성자의 파라미터에 Comparator 를 구현해서 정렬을 정의할 수 있음.




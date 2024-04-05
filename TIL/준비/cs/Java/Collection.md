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
	저장용량을 넘어서면 자동으로 증가시킴. 

**LinkedList**
* 노드(객체) 끼리의 주소 포인터를 서로 가리키며 링크(참조)함으로써 이어지는 구조를 가짐.

**Vector**
* JDK 1.0 부터 있었던 자료 구조, 호환성을 위해 남겨 놓은 레거시 클래스
* Vector는 ArrayList와 기능상 거의 동일하지만, 다른점이 있음
	ArrayList는 비동기 방식, Vector 는 동기 방식


**Stack**
* Vector 를 상속하여 사용하는 LIFO(Last In First Out) 방식의 클래스
* Java 에서는 Stack 대신 Deque 를 사용하여 구현할 것을 권장함.

**Queue**
* FIFO 구조를 가진 자료구조
* LinkedList 를 이용하여 구현할 수 있음
* Deque 와 PriorityQueue 가 있음.


**Set**
* 중복된 요소를 저장하지 않고, 요소의 저장 순서를 유지하지 않는 특징을 가짐.
* 구현체로 HashSet, LinkedHashSet, TreeSet 이있음.

**HashSet**
* Set 을 이용하기 위해 가장 많이 사용하는 구현 클래스 
* 해시 알고리즘을 사용하여 검색속도가 빠르다.
* HashSet 의 인스턴스는 HashMap 의 인스턴스를 통해 생성


**LinkedHashSet**
* HashSet과 원리는 같으나, 입력된 순서를 저장
* HashSet의 상속을 받으며, LinkedHashMap을 통해 구현되어 있음

**TreeSet**
* 특정 기준에 따라 요소를 정렬할 수 있음.
* 생성자의 파라미터에 Comparator 를 구현해서 정렬을 정의할 수 있음.

**Map**



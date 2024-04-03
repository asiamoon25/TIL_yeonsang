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

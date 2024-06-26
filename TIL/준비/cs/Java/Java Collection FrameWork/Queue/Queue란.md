---
sticker: emoji//1f3f8
---
### Queue 란?
* 한쪽 끝 에서만 삽입이 이루어지고, 다른 한쪽 끝에서는 삭제 연산만 이루어지는 유한 순서 리스트


### Queue 의 특징
* **FIFO(First In First Out)**
	선입선출 형태를 가짐.
* Queue 는 한쪽에서는 데이터가 추가되고 한쪽에서는 데이터가 삭제되는 구조를 가짐.
* Queue 의 용어
	* **삽입(Enqueue)** 이 일어나는 곳을 **Rear**
	* **삭제(Dequeue)** 가 일어나는 곳을 **Front**
* 장점
	* 데이터가 입력된 시간 순서대로 처리해야 할 필요가 있는 상황에 유리
	* 데이터 접근 삽입 삭제가 빠르다.
* 단점
	* 크기가 제한적
	* 중간에 위치한 데이터에 대한 접근이 불가능함.

### Queue 의 종류

#### Linear Queue(선형 큐)
![[Pasted image 20240412210036.png]]
* 기본적인 큐의 형태
* 막대 모양으로 된 Queue로, 크기가 제한되어 있고 빈 공간을 사용하려면 모든 자료를 꺼내거나 자료를 한칸 씩 옮겨야 한다는 단점이 있음.

#### Circular Queue (원형 큐)
![[Pasted image 20240412210016.png]]
* 선형 큐의 문제점을 보완한 큐
* 배열의 마지막 인덱스에서 다음 인덱스로 넘어갈 때 (`index + 1) % 배열의 사이즈` 를 통해 0으로 순환되는 구조를 가짐.

#### Priority Queue(우선순위 큐)
* 들어간 순서에 상관 없이 **우선순위가 높은 데이터가 먼저 나오는** 큐
* 우선순위가 높은 데이터를 먼저 Dequeue 하는 특성을 위해 내부의 **heap** 이라는 완전 이진트리 자료구조를 통해 우선순위를 유지함.

### Queue 의 구현
*  Queue 의 구현 방법
	* 배열(Array) 를 이용해 구현
		* 장점
			- 배열 내 요소의 주소를 나타내는 인덱스를 통해 원하는 데이터를 빠르게 검색하여 접근 가능
		- 단점
			- 선언할 때 크기가 고정되어 배열에 들어있는 데이터 양에 따라 배열의 크기 조정이 필요
			- 데이터를 중간에 삽입하거나 삭제할 경우 해당 데이터 뒤에 있는 요소들의 위치를 모두 이용시켜야하는 비효율적인 상황이 발생함.
	- 연결리스트(LinkedList) 를 이용해 구현
		- 장점
			- 데이터의 양에 상관없이 크기가 동적으로 변경
			- 인덱스 대신 이전 데이터 그리고 다음 데이터의 위치를 기억하는 노드 형태를 이용하여 데이터 삽입, 삭제 시 노드들 사이에 연결된 링크들을 끊거나 이어주면 되기에 과정이 용이함.
		- 단점
			- 데이터에 접근할 때 연결되어 있는 노드들을 따라 양끝에서 부터 순차적으로 접근해야 하기 때문에 데이터 접근속도가 배열에 비해 느림.


---

### 메소드

| 메소드              | 설명                                                                           |
| ---------------- | ---------------------------------------------------------------------------- |
| add(Object item) | 해당 큐의 맨 뒤에 전달된 요소를 삽입, (성공시 true를 반환, 큐가 full일 경우 IllegalStateException을 발생) |
| element()        | 해당 큐의 맨 앞에 있는 요소를 반환                                                         |
| offer(E e)       | 해당 큐의 맨 뒤에 전달된 요소를 삽입                                                        |
| peek()           | 해당 큐의 맨 앞에 있는 요소를 반환. Empty일 경우 null을 반환                                     |
| poll()           | 해당 큐의 맨 앞에 있는 요소를 반환하고, 해당 요소를 큐에서 제거, Empty일 경우 null을 반환                    |
| remove()         | 해당 큐의 맨 앞에 있는 요소를 제거                                                         |

### 시간복잡도

- LinearQueue
    
    ```시간복잡도
    add             : O(1)
    poll            : O(1)
    peek            : O(1)
    remove          : O(n)
    ```
- PriorityQueue
    
    ```시간복잡도
    add()      : O(log n)
    poll()     : O(log n)
    peek()     : O(1)
    ```
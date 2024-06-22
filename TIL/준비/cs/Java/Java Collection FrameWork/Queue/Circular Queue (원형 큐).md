
## 란?

* **개념**
	* Front 와 Rear 포인터
		* **Front**
			* 큐의 맨 앞 요소를 가리키는 포인터
		* **Rear**
			* 큐의 마지막 요소를 가리키는 포인터
	* **원형 연결**
		* Rear 포인터가 배열의 끝에 도달하면, 그 다음 위치는 배열의 첫 번째 요소가 됨. 즉 `Rear` 가 `n-1` 에서 `n`으로 증가할 때, 다시 `0` 으로 돌아옴.
	* **공간 효율성**
		* Circular Queue 는 배열의 고정된 크기 내에서 효율적으 메모리를 사용함. 특히, 큐의 빈 공간을 최소화할 수 있음.


## 작동 방식

1. **초기화**
	* 큐를 초기화 할 때, `Front`  와 `Rear` 는 -1 또는 특정 초기 값으로 설정됨.

2. **삽입(Enqueue)**
	* 요소를 큐에 삽입할 때 `Rear` 포인터를 증가시키고, 해당 위치에 요소를 저장함.
	* 만약 `Rear` 가 배열의 끝에 도달했다면, `Rear` 는 0으로 설정됨.

3. **삭제(Dequeue)**
	* 요소를 큐에서 삭제할 때 `Front` 포인터를 증가시키고, 해당 위치의 요소를 제거함.
	* 만약 `Front` 가 배열의 끝에 도달했다면, `Front` 는 0으로 설정ㅚㅁ.

4. **빈 큐 확인**
	* `Front` 와 `Rear` 가 동일한 큐가 비어있음을 의미함.(초기 상태 혹은 모든 요소가 삭제된 상태)

5. **포화 큐 확인**
	* `Rear` 가 `Front-1` 에 위치하거나, `Front` 가 0이고 `Rear` 가 배열의 끝에 있는 경우 큐가 포화 상태임을 의미함.


```java
public class CircularQueue {
	private int size;
	private int front;
	private int rear;
	private int[] queue;
	
	//Circular Queue 초기화
	public CircularQueue(int size) {
		this.size = size;
		this.front = -1;
		this.rear = -1;
		this.queue = new int[size];
	}
	
	// 큐가 비어 있는지 확인
	public boolean isEmpty() {
		retur front == -1;
	}
	
	// 큐가 가득 찼는지 확인
	public boolean isFull() {
		return (rear + 1) % size == front;
	}
	
	// 요소 삽입
	public void enqueue(int item) {
		if(isFull()) {
			throw new RuntimeException("Queue is full");
		}
		if(isEmpty()) {
			front = 0;
		}
		rear = (rear + 1) % size;
		queue[rear] = item;
	}
}
```

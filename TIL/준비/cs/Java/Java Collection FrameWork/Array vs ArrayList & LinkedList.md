#JavaCollectionFramework #Array #ArrayList #LinkedList

_JavaCollectionFramework 에 Array 빼고 ArrayList, LinkedList 넣어놓음 _

# Array vs ArrayList vs LinkedList

## Array
### 정의
배열은 고정 크기를 가지며, 같은 타입의 요소를 메모리의 연속적인 위치에 저장함.
```java
int[] arr = new int[n];
char[] arr = new char[n];
double[] arr = new double[n];
float[] arr = new float[n];
...
```

### 장점
* 인덱스를 통해 빠른 접근이 가능 (`O(1)`)
* 기본적인 데이터 구조로 메모리 사용이 효율적

### 단점
* 크기가 고정되어 있어, 배열을 생성할 때 최대 크기를 미리 정해야 하며, 크기 조정이 불가능하다.
* 요소의 추가 및 삭제가 비효율적임.(중간에 요소를 추가하거나 삭제할 경우, 나머지 요소를 이동해야함.)

## ArrayList
[ArrayList 정리한거](obsidian://open?vault=TIL_yeonsang&file=TIL%2F%EC%A4%80%EB%B9%84%2Fcs%2FJava%2FJava%20Collection%20FrameWork%2FList%2FArrayList)
### 정의
`ArrayList` 는 가변크기를 가지며, 내부적으로 배열을 사용해 데이터를 저장함. 필요에 따라 자동으로 크기를 조정

### 장점
* 인덱스를 통한 접근이 빠름 ( `O(1)` )
* 데이터의 동적 추가 및 삭제가 가능

### 단점
* 크기 조정 과정에서 데이터를 새 배열로 복사해야 하므로, 크기 조정 비용이 발생할 수 있음. ( `O(n)` )
* 요소들이 메모리에 연속적으로 위치하기 때문에, 중간에 요소를 추가하거나 삭제하는 작업은 비효율적일 수 있음.


## LinkedList
[LinkedList 정리한거](obsidian://open?vault=TIL_yeonsang&file=TIL%2F%EC%A4%80%EB%B9%84%2Fcs%2FJava%2FJava%20Collection%20FrameWork%2FList%2FLinkedList)

### 정의
`LinkedList` 는 요소들이 포인터로 서로 연결되어 있는 구조를 가짐. 각 요소(노드) 는 데이터와 다음 노드를 가리키는 포인터를 가지고 있음.

### 장점
* 데이터의 추가 및 삭제가 용이함. 특정 위치에서의 추가나 삭제는 `O(1)` 의 시간이 소요됨.
* 동적 크기 조정이 필요 없음.

### 단점
* 인덱스를 통한 무작위 접근이 느림 ( `O(n)` ), 모든 요소를 순차적으로 탐색해야 함.
* 각 요소가 추가적인 포인터 정보를 저장해야 하므로, 메모리 사용이 비효율적일 수 있음.

---

## 결론
* 고정된 크기의 데이터를 다룰 때는 `Array` 가 적합
* 동적 배열이 필요하고, 빠른 인덱스 접근이 중요한 경우는 `ArrayList` 가 유리함.
* 데이터의 추가 및 삭제가 빈번하게 일어나는 위치 에서는 `LinkedList` 가 더 효율적임.
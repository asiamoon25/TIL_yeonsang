## Hash Table

* Hash 함수를 사용하여 변환한 값을 Index 로 삼아 key 와 value 를 저장하는 자료구조
* 기본연산으로 search, inset, delete 가 있음.

![[Pasted image 20240514151619.png]]
### hash 함수
* 키를 입력으로 받아 해시값을 출력함. 해시값은 보통 정수로, 해시 테이블의 인덱스로 사용됨. 좋은 해시 함수는 충돌(Collision)을 최소화해야함.
* hash(key) % table_size -> key 를 해시하고 테이블 크기로 나눈 나머지를 인덱스로 사용)

### 충돌(Collision)
* 서로 다른 키가 같은 해시값을 가질 때 발생함. 이는 해시 함수가 완벽하지 않기 때문임.
* key1 과 key2 가 hash(key1) == hash(key2) 인 경우

## 충돌 처리 방법

1. chaining
	* 각 버킷에 연결 리스트를 사용하여 충돌을 처리함. 충돌이 발생하면 해당 버킷 리스트에 새로운 요소를 추가함.
	* 장점 : 테이블이 꽉 차지 않음.
	* 단점 : 연결 리스트의 길이가 길어지면 성능 저하

2. 오픈 어드레싱(Open Addressing)
	* 충돌이 발생하면 다른 빈 버킷을 찾아 값을 저장함. 대표적인 방법으로 선형 탐사(Linear Probing), 제곱 탐사(Quadratic Probing), 이중 해싱(Double Hashing) 이 있음.
	* 선형 탐사 : 충돌 시 한 칸씩 이동
	* 제곱 탐사 : 충돌 시 제곱 수 만큼 이동
	* 이중 해싱 : 두 번째 해시 함수를 사용하여 이동

## 시간 복잡도
* 평균 시간복잡도 : O(1)
	* 해시 테이블은 평균적으로 삽입, 삭제, 검색 연산이 O(1) 의 시간 복잡도를 가짐.

* 최악 시간 복잡도 : O(n)
	* 모든 키가 같은 해시값을 가질 때 발생하는 최악의 경우

**예제**
```java
import java.util.LinkedList;

class HashTable<K, V> {
    private class HashNode<K, V> {
        K key;
        V value;
        HashNode<K, V> next;
        
        public HashNode(K key, V value) {
            this.key = key;
            this.value = value;
            this.next = null;
        }
    }
    
    private LinkedList<HashNode<K, V>>[] chainArray;
    private int M = 11;  // 테이블 크기
    private int size;
    
    public HashTable() {
        chainArray = new LinkedList[M];
        size = 0;
        for (int i = 0; i < M; i++) {
            chainArray[i] = new LinkedList<HashNode<K, V>>();
        }
    }
    
    private int hash(K key) {
        return Math.abs(key.hashCode() % M);
    }
    
    public void insert(K key, V value) {
        int bucketIndex = hash(key);
        LinkedList<HashNode<K, V>> chain = chainArray[bucketIndex];
        for (HashNode<K, V> node : chain) {
            if (node.key.equals(key)) {
                node.value = value;
                return;
            }
        }
        chain.add(new HashNode<>(key, value));
        size++;
    }
    
    public V search(K key) {
        int bucketIndex = hash(key);
        LinkedList<HashNode<K, V>> chain = chainArray[bucketIndex];
        for (HashNode<K, V> node : chain) {
            if (node.key.equals(key)) {
                return node.value;
            }
        }
        return null;
    }
    
    public boolean delete(K key) {
        int bucketIndex = hash(key);
        LinkedList<HashNode<K, V>> chain = chainArray[bucketIndex];
        for (HashNode<K, V> node : chain) {
            if (node.key.equals(key)) {
                chain.remove(node);
                size--;
                return true;
            }
        }
        return false;
    }
    
    public int size() {
        return size;
    }
    
    public boolean isEmpty() {
        return size() == 0;
    }
}

public class Main {
    public static void main(String[] args) {
        HashTable<String, Integer> hashTable = new HashTable<>();
        hashTable.insert("apple", 1);
        hashTable.insert("banana", 2);

        System.out.println(hashTable.search("apple"));  // 출력: 1
        System.out.println(hashTable.search("banana"));  // 출력: 2
        System.out.println(hashTable.search("grape"));  // 출력: null

        hashTable.delete("apple");
        System.out.println(hashTable.search("apple"));  // 출력: null
    }
}
```

1. HashNode 클래스
	* key - value 쌍을 저장하는 노드 클래스임. 각 노드는 다음 노드를 가리키는 포인터('next') 를 가지고 있음.

2. HashTable 클래스
	* 체이닝을 사용하여 충돌을 처리하는 해시 테이블 클래스
	  
	* chainArray 는 LinkedList 배열로, 각 인덱스는 하나의 체인을 가리킴.
	  
	* 'M' 은 테이블 크기
	  
	* hash 메서드는 키의 해시값을 계산하여 배열 인덱스를 반환함.
	  
	* insert 메서드는 키 -값 쌍을 해시 테이블에 삽입함. 충돌이 발생하면 체인의 끝에 노드를 추가함.
	  
	* search 메서드는 키에 해당하는 값을 검색하여 반환함. 키가 존재하지 않으면 null 을 반환함.
	  
	* delete 메서드는 키에 해당하는 노드를 삭제함. 삭제가 성공하면 true 실패하면 false 를 반환함.
	  
	* size 메서드는 해시테이블의 현재 크기를 반환함.
	  
	* isEmpty 메서드는 해시 테이블이 비어 있는지 확인함.



## 장단점

* 장점
	* 빠른 데이터 접근 속도(평균적으로 O(1))
	* 간단한 구현 및 이해

* 단점 
	* 충돌이 발생하면 성능 저하
	* 해시 함수의 품질에 따라 성능이 크게 좌우됨.


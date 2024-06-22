
## 란? 

`ConcurrentHashMap` 은 Java 의 Collection Framework 에서 멀티 스레드 환경에서 안전하게 사용할 수 있는 고성능의 Map의 구현체임.
`HashMap` 과 유사하지만, 동시성을 제공하여 여러 스레드가 동시에 안전하게 데이터를 읽고 쓸 수 있게 설계되었음.

## 원리

`ConcurrentHashMap` 은 내부적으로 다양한 최적화 기법을 사용하여 동시성을 관리함.

1. **Segment Locks**
	* Java 7 까지는 `ConcurrentHashMap` 이 여러 개의 세그먼트로 나누어져 각 세그먼트에 별도의 락을 적용함.
	* Java 8 이후에는 더 세분화된 버킷 단위로 락을 적용하여 동시성을 더욱 향상 시켰음.

2. **CAS(Compare-And-Swap) 연산**
	* 원자적 연산을 위해 CAS 연산을 사용함. 이는 락을 걸지 않고도 안전하게 값을 변경할 수 있도록 함.

3. **트리화(Treeify)**
	* 해시 충돌이 많은 경우, 연결 리스트 대신 트리 구조로 변환하여 검색 성능을 향상시킴.

4. **락 스트라이핑(Lock Stripping)**
	* 락을 세분화하여 필요한 부분에만 적용함으로써 락 경합을 최소화하고 성능을 향상시킴.

## 특징

* **동시성**
	* 여러 스레드가 동시에 안전하게 접근할 수 있도록 설계되었음.

* **세분화된 락**
	* 락의 범위를 최소화하여 성능을 향상시킴.

* **원자적 연산 지원**
	* `putIfAbsent`, `remove`, `replace` 등의 메서드를 통해 원자적 연산을 지원함.

* **Null 키와 값 허용 안 함**
	* Null 키와 값을 허용하지 않음.

* **트리화**
	* 해시 충돌이 많은 경우 트리로 변환하여 성능을 유지함.


## 장단점

**장점**
* **높은 동시성**
	* 세분화된 락 덕분에 여러 스레드가 동시에 안전하게 접근할 수 있음.
* **성능**
	* 멀티스레드 환경에서 매우 높은 성능을 제공함.
* **원자적 연산**
	* 원자적 연산을 통해 복잡한 동기화 코드를 작성할 필요가 없음.

**단점**
* **메모리 사용량**
	* 내부적으로 더 많은 구조를 사용하므로 메모리 사용량이 많을 수 있음.
* **Null 값 미허용**
	* Null 키와 값을 허용하지 않으므로 사용 시 주의가 필요함.


## 언제 써야함?

* **멀티스레드 환경**
	* 여러 스레드가 동시에 맵에 접근하고 수정하는 경우
* **고성능이 필요한 경우**
	* 동기화가 필요한 경우 성능 저하를 최소화해야 할 때
* **원자적 연산이 필요한 경우**
	* 복잡한 동기화 코드를 작성하지 않고도 원자적 연산을 수행해야 할 때.


## 시간복잡도
* **삽입,삭제 조회**
	* 평균적으로 O(1) 임. 트리로 변환된 경우 최악의 경우 O(log n) 임.



## 내부 메서드

* `put(K key, V value)`
	* 지정된 키와 값을 맵에 삽입함.
* `get(Object key)` 
	* 지정된 키에 대응하는 값을 반환함.
* `remove(Object key)`
	* 지정된 키가 맵에 없을 경우에만 값을 삽입함.
* `replace(K key, V oldValue, V newValue)`
	* 지정된 키와 기존 값을 새로운 값으로 교체함.
* `computeIfAbsent(K key, Function<? super K, ? extends V> mappingFunction)`
	* 지정된 키가 맵에 없을 경우 주어진 함수에 따라 값을 계산하고 삽입함.
* `computeIfPresent(K key, BiFunction<? super K, ? super V, ? extends V> remappingFunction)`
	* 지정된 키가 맵에 존재할 경우 주어진 함수에 따라 값을 재계산하고 업데이트함.
* `compute(K key, BitFunction<? super K, ? super V, ? extends V> remappingFunction)`
	* 지정된 키에 대해 주어진 함수에 따라 값을 계산하고 업데이트함.

**예제**
```java
public class ConcurrentHashMapExample {
	public static void main(String[] args) {
		ConcurrentHashMap<String, String> map = new ConcurrentHashMap<>();
		
		//값을 삽입
		map.put("key1", "value1");
		map.put("key2", "value2");
		
		// 기존 키가 없으면 값을 삽입
		map.putIfAbsent("key3", "value3");
		
		//값 가져오기
		System.out.println("key1: " + map.get("key1"));
		
		//값 교체
		m
	}
}
```
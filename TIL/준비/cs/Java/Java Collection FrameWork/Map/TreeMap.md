#JavaCollectionFramework #Map #TreeMap

## TreeMap 이란?

* Collection Framework 의 일부로 `Map` 인터페이스를 구현하는 red-black tree 기반의 NavigableMap 구현
* key-value 를 저장하며, 모든 엔트리는 key 에 따라 자동으로 정렬됨.
	* type 이 숫자일 경우 값으로, 문자일 경우 유니코드로 정렬함.
	* 정렬 순서는 기본적으로 부모 key 값과 비교해서 key 값이 낮은 것은 왼쪽 자석 노드에 key 값이 높은 것은 오른쪽 자식 노드에 Map.Entry 객체를 저장함.

## 특징
1. 정렬된 순서
	`TreeMap` 은 key 에 따라 자동으로 정렬됨. 기본적으로는 key 의 자연적 순서를 사용하거나, 생성자에 Comparator 를 제공하여 정렬 순서를 사용자가 정의할 수 있음.
2. key 기반 검색
	`TreeMap` 은 key 를 사용하여 빠르게 검색할 수 있게 해주며, `get`, `put`, `remove` 같은 메서드를 통해 이루어짐
3. 시간 복잡도
	`TreeMap` 의 검색, 삽입, 삭제 연산은 모두 평균적으로 O(log n) 시간 복잡도를 가짐. n 은 Tree 의 노드 수
4. NavigableMap 인터페이스
	`TreeMap` 은 `NavigableMap` 인터페이스를 구현함으로써, key 에 대한 탐색(예 : 가장 가까운 key 찾기, 범위 검색 등) 에 유용한 메서드를 제공함.
5. 범위 검색과 순회
	key 의 자연적 순서를 활용하여, 특정 범위의 key 에 대한 부분 맵 또는 key-value 의 집합을 빠르게 검색하고 순회할 수 있음.

> TreeMap 은 일반적으로 Map 으로써 성능이 HashMap 보다 떨어짐.
> TreeMap 은 데이터를 저장할 때 즉시 정렬하기에 추가나 삭제가 HashMap 보다 오래 걸림.
> 하지만 정렬된 상태로 Map 을 유지해야 하거나 정렬된 데이터를 조회해야 하는 범위 검색이 필요한 경우 TreeMap 을 사용하는 것이 효율성면에서 좋음.


## Red-Black Tree

Red-Black Tree 는 자가 균형 이진 탐색 트리의 일종으로, 각 노드가 빨간색 또는 검은색의 추가 속성을 가지고 있는 특징을 가짐.

Red-Black Tree 에 관해서는 자세하게 다른 곳에다가 적음.


---
## 메서드

TreeMap 은 Map 인터페이스의 구현이면서 NavigableMap 구현이기도 하다.

### 기본 `Map` 인터페이스 메서드
* `put(K key, V value)` : 지정된 key 에 value 를 연결함. 이미 해당 key 값이 있으면, 그 값을 새값으로 대체
* `get(Object key)` : 지정된 key 에 연결된 value 를 반환함. key가 Map 에 없으면 null 을반환함.
* `remove(Object key)` : 지정된 key 와 그에 해당하는 값을 제거함.
* `containsKey(Object key)` : 지정된 key 가 Map 에 있는지 확인함.
* `containsValue(Object value)` : 지정된 값이 Map 에 있는지 확인함.
* `size()` : 맵에 있는 key-value 쌍의 수를 반환
* `isEmpty()` : Map 이 비어 있는지 확인함.
* `clear()` : Map 에 모든 값을 제거함.

### `NavigableMap` 인터페이스 메서드
* `firstEntry()` : 맵에서 가장 작은 key 를 가진 Entry 를 반환함.
* `lastEntry()` : 맵에서 가장 큰 key 를 가진 Entry 를 반환함.
* `pollFirstEntry()` : 맵에서 가장 작은 키를 가진 엔트리를 제거하고 반환함.
* `pollLastEntry()` : 맵에서 가장 큰 키를 가진 Entry 리를 제거하고 반환함.
* `higherEntry(K key)` : 지정된 key 보다 바로 더 큰 key 를 가진 엔트리를 반환함.
* `lowerEntry(K key)` : 지정된 키보다 바로 더 작은 key 를 가진 엔트리를 반환함.
* `ceilingEntry(K key)` : 지정된 key 와 같거나 더 큰 key 중 가장 작은 key 를 가진 엔트리를 반환함.
* `floorEntry(K key)` : 지정된 key 와 같거나 더 작은 key 중 가장 큰 key 를 가진 엔트리를 반환함.

### 정렬과 관련된 메서드
* `subMap(K fromKey, boolean fromInclusive, K toKey, boolean toInclusive)` : 지정된 범위 내의 부분 Map 을 반환함.
* `headMap(K toKey, boolean inclusive)` : 지정된 Key 보다 작은 key 들을 가진 부분 맵을 반환함.
* `tailMap(K fromKey, boolean inclusive)` : 지정된 key 보다 크거나 같은 key 들을 가진 부분 Map 을 반환함.
#Map #HashMap #JavaCollectionFramework 

# HashMap


## 이란?
* Map 인터페이스를 구현하고 있는 대표적인 클래스
* key, value 쌍으로 구성되어 있음.
* 하나의 key 당 하나의 value 를 가질 수 있음.
* 해싱(Hashing) 검색을 사용하기 때문에 데용량 데이터 관리에도 좋은 성능을 보여줌.

## 특징
* key 의 고유성 : 각 key는 `Map` 내에서 유일해야함. 같은 key 로 새로운 값을 `put` 하면 기존의 값이 새로운 값으로 대체됨.
* 순서 보장 안됨 : `HashMap` 은 데이터의 순서를 보장하지 않음. 넣은 순서와 `Map` 을 순회할 때 나오는 순서가 다를 수 있음.
* null 값 허용 : `HashMap` 은 key 와 value 값으로 `null` 을 허용함. 하나의 `null` 키와 여러 `null` 값들을 저장할 수 있음.
* Thread-safe 하지 않음 : `HashMap` 은 멀티 쓰레드 환경에서 동시에 수정될 경우 데이터의 일관성을 보장하지 않음. 멀티 쓰레드에서는 `ConcurrentHashMap` 을 사용하는게 좋음.


---

## 메소드

* put(K key, V value) : key 와 value 값을 `Map` 에 추가함. 이미 존재하는 key 에 값을 추가하면, value 교체됨.
* get(Object key) : 지정된 키에 연결된 값을 반환함. key 가 `Map` 에 없는 경우 `null` 을 반환함.
* remove(Object key) : 지정된 Key 와 그에 연결된 값을 `Map` 에서 제거함.
* containsKey(Object key) : `Map` 에 지정된 key 가 있는지 true, false 를 반환
* containsValue(Object value) :  `Map` 에 지정된 value 가 하나라도 있는지 true,false 를 반환
* size() : `Map` 에 저장된 key-value 쌍의 수를 반환
* isEmpty() : `Map` 이 비어 있는지 여부를 확인
* clear() : `Map` 에서 모든 키와 값을 여부를 확인
* keySet() : `Map` 에 있는 모든 key 를 `Set` 형태로 반환
* values() : `Map` 에 있는 모든 값을 Collection 형태로 반환
* entrySet() : `Map` 에 있는 모든 key-value 쌍을 `Set` 의 `Map.Entry<K, V>` 형태로 반환

---

`HashMap` 은 key 를 통해 빠르게 값을 검색해야할 때 유용하다. 특히 데이터를 key-value 쌍으로 관리해야하는 다양한 프로그래밍에서 사용됨.
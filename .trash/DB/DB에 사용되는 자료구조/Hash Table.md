## Hash Table 이란?
* 검색하고자 하는 키 값을 입력받아서 Hash 함수를 통해 얻은 Hash를 배열의 인덱스로 환산해서 데이터에 접근하는 자료구조
* Direct Address Table 과는 달리 Key k 가 slot h(k) 에 들어가게 됨.
	![[Pasted image 20231213170428.png]]

### h(k) 함수
* Division Method
	* 나눗셈을 이용한다. 입력값을 테이블의 크기로 나누어 계산 
		(주소 = 입력값 % 테이블의 크기)
		테이블의 크기를 소수로 정하고 2의 제곱수와 먼 값을 사용해야 효과가 좋다고 알려져 있음.
* Digit Folding
	* 각 Key 의 문자열을 ASCII 코드로 바꾸고 값을 합한 데이터를 테이블 내의 주소로 사용
* Multiplication Method
	* 숫자로 된 Key 값 K 와 0과 1 사이의 실수 A, 보통 2의 제곱수인 m 을 사용하여 계산함
		h(k) = (kAmod1) x m
		mod = % (나머지)
		kAmod1 => k x A % 1 => kA 의 소수점 이하 자리
* Universal Hashing
	* 다수의 해시 함수를 만들어 집합 H 에 넣얻두고, 무작위로 해시함수를 선택해 해시값을 만드는 기법


## 충돌

* value1 을 해시를 돌려 나온 값과 value2 를 돌려 나온 값이 동일하다면 충돌이 일어남.

### 충돌 해결법

**1. 분리 연결법**
	동일 버킷 의 데이터에 대해 자료구조를 활용해 추가 메모리를 사용하여 다음 데이터의 주소를 저장.
	Chaining 방식은 Hash Table 의 확장이 필요 없고 간단하게 구현이 가능, 삭제도 쉽다.
	데이터 수가 많아지면 chaining 데이터가 많아지며 캐시의 효율성이 감소한다.

**2. 개방주소법**
	비어있는 Hash Table 의 공간을 활용하는 방법 
	1. Linear Probing 
		현재의 버킷 index 로 부터 고정폭 만큼씩 이동하며 비어있는 버킷에 데이터를 저장함.
	2. Quadratic Probing
		Hash의 저장순서 폭을 제곱으로 저장하는 방법.
			처음 충돌이 발생한 경우에는 1만큼 그 다음 충돌 시 2^2, 3^2 칸씩 옮기는 방법
	3. Double Hashing Probing
		Hash 된 값을 한번 더 Hashing 하여 Hash 의 규칙성을 없애버리는 방식
			Hash 된 값을 한번 더 Hashing 하여 새로운 주소를 할당하기 때문에 다른 방법들보다 많은 연산을 하게 된다.
	![[Pasted image 20231213175843.png]]
	Open Addressing에서 데이터를 삭제하면 삭제된 공간은 Dummy Space로 활용되는데, 그렇기 때문에 Hash Table을 재정리 해주는 작업이 필요하다고 함.

## Hash Table 의 시간복잡도

* 각각의 Key 값은 Hash 함수에 의해 고유한 index를 가지게 되어 바로 접근할 수 있으므로 평군 O(1) 의 시간복잡도로 데이터를 조회할 수 있음.
	하지만 데이터의 충돌이 발생한 경우 Chaining에 연결된 리스트들까지 검색을 해야하기 때문에 O(N) 까지 시간복잡도가 증가할 수 있음.
	
	충돌을 방지하는 방법들은 데이터의 규칙성(클러스터링) 을 방지하기 위한 방식이지만 공간을 많이 사용한다는 치명적인 단점이 있음.
	
	만약 테이블이 꽉 차있는 경우라면 테이블을 확장해주어야 하는데, 이는 매우 심각한 성능의 저하를 불러오기 때문에 가급적이면 확장을 하지 않도록 테이블을 설계해야함.
		통계적으로 Hash Table 의 공간 사용률이 70 ~ 80 % 정도가 되면 Hash 의 충돌이 빈번하게 발생하여 성능이 저하되기 시작함. 
	
	Hash 테이블에서 자주 사용하게 되는 데이터를 Cache에 적용하면 효율을 높일 수 있음.

## Java에서 HashMap 과 Hash Table 의 차이점
* 동기화 지원 차이

**JAVA의 Hashtable**
```java
public synchronized V get(Object key) {  
	Entry<?,?> tab[] = table;  
	int hash = key.hashCode();  
	int index = (hash & 0x7FFFFFFF) % tab.length;  
	for (Entry<?,?> e = tab[index] ; e != null ; e = e.next) {  
		if ((e.hash == hash) && e.key.equals(key)) {  
		return (V)e.value;  
		}  
	}  
	return null;  
}
```

**JAVA의 HashMap**
```java
public V put(K key, V value) {  
return putVal(hash(key), key, value, false, true);  
}
```

동기화 처리 -> 병렬처리에 사용, 대신 함수 처리에 시간이 좀 걸린다.

병렬 처리 하면서 자원의 동기화를 고려하는 상황이라면 HashTable 아니면 HashMap
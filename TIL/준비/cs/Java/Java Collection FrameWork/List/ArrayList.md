---
sticker: emoji//1f6a1
---
**ArrayList**
* 크기가 가변적인 선형 리스트, 저장용량이 존재함.  
	저장용량을 넘어서면 자동으로 증가시킴. 
* 특징
	1. 연속적인 데이터의 리스트(빈공간이 있으면 안됨.)
	2. 타입 안정성
		* ArrayList 는 제네릭을 사용하여 타입 안정성을 제공함.
		  ArrayList\<String\>  은 문자열만 저장할 수 있도록 함.
	3. 인덱스를 통한 빠른 접근
		ArrayList 는 인덱스를 사용하여 배열 요소에 빠르게 접근할 수 있음.
		데이터 검색이나 업데이트 시 유용함.
	4. 데이터 조작
		* ArrayList 는 요소를 추가, 삭제, 검색, 정렬 등 다양한 방법으로 데이터를 조작할 수 있는 메소드를 제공

**ArrayList vs 배열**

* 배열 장단점
	* **장점**
		1. 빠른 데이터 접근 : 배열은 인덱스를 통해 각 요소에 대한 빠른접근이 가능. 배열 요소를 읽거나 쓸 때 O(1) 의 시간복잡도를 가짐.
		2. 메모리 효율성 : 배열은 메모리를 연속적으로 사용하기 때문에 메모리 관리의 관점에서 효율적
		3. 간단한 구현 : 배열의 구현이 간단하기 때문에, 사용하기 쉽고 이해하기도 쉬움.
	* **단점**
		1. 고정된 크기 : 배열은 생성 시에 지정된 크기를 변경할 수 없음(정적할당)
		2. 삽입과 삭제의 비효율성 : 배열의 중간에 요소를 삽입하거나 삭제할 경우, 나머지 요소들을 이동시켜야 하기 때문에 O(n) 의 시간 복잡도를 가짐
		3. 메모리 낭비 : 배열의 크기를 정할 때 예측이 어려움

* ArrayList 장단점
	* **장점**
		1. 동적 크기 조정 : ArrayList의 요소가 추가될 때 내부 배열 크기가 부족하면 자동으로 크기 조정
		   
		2. 인덱스를 통한 빠른 접근 : 배열 기반이기 때문에 특정 인덱스의 요소에 대한 접근이 매우 빠름(일반적으로 O(1) 의 시간 복잡도)
		   
		3. API 편리성 : ArrayList는 List 인터페이스의 메소드들을 상속받기 때문에 다양하고 편리한 API를 제공(검색, 정렬, 순회 등)
		   
	* **단점**
		1. 삽입과 삭제의 비효율성 : 배열과 비슷
		   
		2. 메모리 오버헤드 : 내부적으로 배열을 사용하여 데이터를 저장하기 때문에 크기 조정 시 현재 배열의 크기보다 큰 새배열을 생성하고 기존의 데이터를 복사하기 때문에, 잠시동안 추가적인 메모리를 사용
		   
		3. 동기화 되지 않음 : ArrayList 는 동기화가 되지 않음.->synchronized 가 없음... 대신 동기화를 위해서 Collections.synchronizedList(new ArrayList(...)); 를 해주면 됨.

**ArrayList , 배열 비교점**
* 타입 안정성 : 배열은 동일한 타입의 데이터만 저장가능, 배열은 Object 객체 타입만 저장할 수 있음. 기본 데이터 타입은 Wrapper 클래스 를 사용해야함.
  
* 크기 조정 : 배열은 고정 크기 , ArrayList 는 동적으로 조절 가능.
  
* 성능 : 배열은 크기가 고정되있고 메모리에 연속적으로 할당되기 때문에 데이터에 접근하는데 있어 ArrayList 보다 빠를 수 있음.
  
* 편의성 : ArrayList 는 add, remove, contains 등 다양한 메서드를 제공함.

---
## 메소드

### 데이터 추가

* **add(Object e)** : 지정된 요소를 리스트의 끝에 추가
```java
ArrayList<String> fruits = new ArrayListM<String>();
fruits.add("Apple");
fruits.add("Apple1");
fruits.add("Apple2");
fruits.add("Apple3");
```
* **add(int index, Object e)** : 지정된 index 에 요소를 추가. 이 위치와 이후의 요소들은 오른쪽으로 한칸 씩 이동함.
```java
fruits.add(1, "Blueberry");
```
* **addAll(Collection c)** : 지정된 컬렉션의 모든 요소를 리스트의 끝에 추가
```java
ArrayList<String> colors = new ArrayList<String>();
colors.add("Red");
colors.add("Blue");

fruits.addAll(colors);
```
* **addAll(int index, Collection c)** : 지정된 컬렉션의 모든 요소를 리스트의 특정 위치부터 추가
```java
fruit.addAll(2,colors);
```
* **set(int index, Object e)** : 리스트의 지정된 위치에 있는 요소를 지정된 요소로 대체함.
```java
fruits.set(2, "Blackberry");
```

### 삭제

* **remove(Object o)** : 지정된 요소를 리스트에서 첫 번째로 발견되는 인스턴스를 삭제
```java
fruits.remove("cherry");
```
* **remove(int index)** : 지정된 위치에 있는 요소를 리스트에서 삭제하고, 그 요소를 반환
```java
fruits.remove(2); 
```
* **clear()** : 리스트의 모든 요소를 삭제
```java
fruits.clear();
```

### 검색

* **get(int index)** : 지정된 위치에 있는 요소를 반환함.
```java
fruits.get(1); // 1 번 위치에 있는 요소 반환
```
* **indexOf(Object o)** : 지정된 요소가 리스트에 처음으로 나타나는 위치를 반환. 리스트의 요소가 없을 경우 -1 을 반환함.
```java
fruits.indexOf("Cherry");
```
* **lastIndexOf(Object o)** : 지정된 요소가 리스트에 마지막으로 나타나는 위치를 반환
```java
fruits.lastIndexOf("Cherry");
```
* **contains(Object o)** : 리스트가 지정된 요소를 포함하고 있는 경우 `true` 를 반환
```java
fruits.contais("Cherry");
```
### 크기 및 상태

* **size()** : 리스트에 있는 요소의 수를 반환
```java
fruits.size();
```
* **isEmpty()** :  리스트가 비어있는 경우 `true` 를 반환함.
```java
fruits.isEmpty();
```
### Iterator

* **iterator()** : 리스트의 요소에 대한 반복자를 반환
```java
Iterator<String> iterator = fruits.iterator();
while(iterator.hasNex()) {
	String fruit = iterator.next();
	 System.out.println(fruit);
}
```
* **listIterator()** : 리스트의 요소에 대한 리스트 반복자를 반환
```java
ListIterator<String> iter = fruits.listIterator();
while(iter.hasNext()) {
	System.out.print (iter.next() + " ");
}
// 1 2 3 4
```
* **listIterator(int index)** : 지정된 위치에서 시작하는 리스트의 요소에 대한 리스트 반복자를 반환
```java
ListIterator<String> iter = fruits.listIterator(2); // 2번째 부터 시작함.

while(iter.hasNext()){
	System.out.println(iterator.next());
}
// Apple2 Apple3 ..
```

### 자르기

* **subList(int fromIndex, int toIndex)** : 리스트의 지정된 범위에 대한 뷰를 반환. 반환된 리스트는 원본 리스트의 변경 사항을 반영함.
```java
List<String> subList = fruits.subList(1,3); // 1 <=  인덱스 <=2
Syste.out.println(subList);
//Apple1, Apple2
```
### 배열전환

* **toArray()** : 리스트의 모든 요소를 포함하는 배열을 반환
```java
Object[] fruitsArray = fruits.toArray();
```
* **toArray(T\[\] a)** : 리스트의 모든 요소를 포함하는 배열을 반환. 지정된 배열이 충분히 크면 그 배열에 요소가 저장됨. 그렇지 않으면, 동일한 런타임 타입의 새 배열이 할당
```java
String[] fruitsArray = fruits.toArray(new String[0])
```
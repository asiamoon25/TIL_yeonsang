---
sticker: emoji//0023-fe0f-20e3
---
## LinkedHashSet

* HashSet 의 순서를 유지하는 버전
* Set 인터페이스의 구현클래스
* HashSet 의 모든 특성을 가지면서도, 추가적으로 요소가 추가된 순서대로 반복할 수 있따는 특징이 있음. 
	LinkedHashSet 이 내부적으로 연결 리스트(Linked List) 를 사용하여 요소의 삽입 순서를 기록하기 때문


## 특징

* 중복이 안됨
	LinkedHashSet 은 동일한 요소의 중복 저장을 허용하지 않음. 각 요소는 집합 내에서 유일

* 삽입 순서 유지
	요소가 추가된 순서대로 요소를 반복할 수 있음. LinkedHashSet 이 요소를 내부적으로 어떤 순서로 저장하고 있는지를 나타냄.

* 빠른 접근 속도
	HashSet 과 마찬가지로, LinkedHashSet 도 해시 테이블을 기반으로 하므로, 요소의 추가, 삭제, 검색 작업이 매우 빠름. 단, HashSet 에 비해 약간 느릴 수 있음.
	삽입 순서를 유지하기 위한 추가적인 Linked List 관리 때문

* null 값 허용
	LinkedHashSet 은 하나의 null 값을 저장할 수 있음.

**사용사례**
	중복을 허용하지 않으면서도 요소의 추가 순서를 유지해야 할 때 유용함.
	사용자가 입력한 고유한 데이터 항목의 순서를 유지하면서 처리해야할 경우가 있음.
```java
LinkedHashSet<String> linkedHashSet = new LinkedHashSet<>();

linkedHashSet.add("Apple");
linkedHashSet.add("Banana");
linkedHashSet.add("Cherry");
linkedHashSet.add("Apple"); // 중복 요소 무시

System.out.println("LinkedHashSet : " + linkedHashSet);

//요소 순서대로 출력
for(String fruit : linkedHashSet) {
	System.out.println(fruit);
}

linkedHashSet.remove("Banana");
System.out.println("After removal: " + linkedHashSet);

//요소의 존재 여부 확인
if(linkedHashSet.contains("Apple")) {
	System.out.println("LinkedHashSet contains Apple");
}
```
이 부분에서 LinkedHashSet 에 여러 과일 이름을 추가하고, 중복된 요소 Apple 을 추가하려하지만, LinkedHashSet 은 중복을 허용하지 않기 때문에 중복 요소는 무시됨.

추가된 순서대로 요소를 출력하면, LinkedHashSet 이 삽입 순서를 어떻게 유지하는지 확인 할 수 있음.

---

## 메서드

#### 추가, 삭제, 검사
* add(E e) : 지정된 요소를 세트에 추가. 요소가 세트에 이미 존재하지 않는 경우에만 추가되며, 추가 성공시 `true` 를 반환함.
* remove(Object o) : 지정된 요소가 세트에 존재하는 경우, 그 요소를 세트에서 제거함. 제거 성공 시 `true` 를 반환함.
* contains()
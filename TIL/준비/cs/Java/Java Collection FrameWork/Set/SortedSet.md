#JavaCollectionFramework  #Set

# SortedSet

## 이란?
* Set 인터페이스를 확장하여 요소들이 정렬된 순서로 유지되는 집합
* 중복을 허용하지 않으면서 모든 요소를 특정 정렬 순서대로 저장


## 특징
* 자동 정렬
	SortedSet 에 요소를 추가하면, 해당 요소는 자동으로 정렬 순서에 따라 적절한 위치에 삽입됨. 정렬순서는 요소의 자연 순서(`Comparable` 인터페이스를 구현) 또는 생성 시 제공된 `Comparator` 에 의해 결정됨.

* 중복 불가
	동일한 요소를 `SortedSet` 에 추가하려고 하면 추가가 무시됨. 즉. `Set` 인터페이스의 특성을 그대로 상속받아 중복된 요소를 저장하지 않음

* 범위 검색
	특정 요소를 기준으로 부분 집합(subset), 머리 집합(headset), 꼬리 집합(tailset) 등을 생성할 수 있으며, 이는 대규모 데이터셋에서 특정 범위의 요소를 효율적으로 처리할 수 있도록 해줌.


---

## 메소드

* first() : 
* last() : 
* headSet(E toElement) : 
* tailSet(E fromElement) : 
* subSet(E fromElement, E toElement) : 
* comparato
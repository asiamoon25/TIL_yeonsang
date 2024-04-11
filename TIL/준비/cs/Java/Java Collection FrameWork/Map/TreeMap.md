#JavaCollectionFramework #Map #TreeMap

## TreeMap 이란?

* Collection Framework 의 일부로 `Map` 인터페이스를 구현하는 red-black tree 기반의 NavigableMap 구현
* key-value 를 저장하며, 모든 엔트리는 key 에 따라 자동으로 정렬됨.
	* type 이 숫자일 경우 값으로, 문자일 경우 유니코드로 정렬함.
	* 정렬 순서는 기본적으로 부모 key 값과 비교해서 key 값이 낮은 것은 왼쪽 자석 노드에 key 값이 높은 것은 오른쪽 자식 노드에 Map.Entry 객체를 저장함.

## 특징
1. 정렬된 순서
	`ㅆ`
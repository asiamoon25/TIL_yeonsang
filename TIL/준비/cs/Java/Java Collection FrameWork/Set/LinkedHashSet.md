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


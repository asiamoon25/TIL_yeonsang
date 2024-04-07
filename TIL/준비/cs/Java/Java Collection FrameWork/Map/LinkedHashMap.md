#Map #LinkedHashMap #JavaCollectionFramework 

## 란?
* HashMap 에 순서를 추가한 형태로 `java.util` 에 속한 녀석임.
* HashMap 의 모든 기능을 포함하면서도, 추가적으로 요소가 추가된 순서 또는 마지막에 접근된 순서를 유지함.


## 특징
* 삽입 순서 유지
	LinkedHashMap 은 요소를 추가한 순서대로 순회함. 내부적으로 double-linked list 를 사용하여 각 요소의 삽입 순서를 기록하기 때문
* 접근 순서 옵션
	생성자에서 `accessOrder` 플래그를 `true` 로 설정하면, `LinkedHashMap` 은 가장 최근에 접근(읽기 또는 쓰기)된 요소를 맨 끝으로 이동시킴. 이는 LRU(Least Recently Used) 캐시를 구현할 때 유용함.
* 성능
	HashMap 과 거의 동일한 성능을 제공함. 삽입과 삭제, 접근 모두 상수 시간 복잡도를 가짐. 순소를 유지하기 위한 추가적인 비용은 매우 작음.
* 용량과 부하계수
	HashMap 과 마찬가지로 LinkedHashMap 도 초기 용량(capacity) 와 부하 계수(load factor) 를 설정할 수 있음. 이는 맵의 성능 튜닝에 사용될 수 있음

## 사용 사례

삽입 순서 또는 접근 순서가 중요한 경우 사용됨. 예를 들어, 캐시, DB 쿼리 결과, 파일의 내용을 순서대로 저장하고 접근해야 할 때 유용함.


---

## 메소드

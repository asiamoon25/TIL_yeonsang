#JavaCollectionFramework  #Set 


# TreeSet


## TreeSet 이란?

*  Set 인터페이스를 구현한 클래스
* 객체를 중복해서 저장할 수 없음
* 저장 순서가 유지되지 않음
* 이진 탐색 트리(BinarySearchTree) 의 구조로 이루어져 있음.
	삭제에는 시간이 조금 더 걸리지만 정렬, 검색에 높은 성능을 보이는 자료구조임
	그래서 HashSet 보다 데이터의 추가와 삭제는 시간이 더 걸리지만 검색과 정렬에는 유리함.
* nature ordering 을 지원하며 생성자의 매개변수로 Comparator 객체를 입력하여 정렬방법을 임의로 지정해줄 수 있음. (asc, desc...)
* 저장 순서가 유지되지는 않지만 정렬된 순서를 유지함.


### 저장 순서가 유지되지는 않지만 정렬된 순서를 유지한다는게..?

Java 의 TreeSet 구현은 실제로 TreeMap 을 내부적으로 사용하여 요소를 저장하고 관리함.
![[Pasted image 20240406194359.png]]



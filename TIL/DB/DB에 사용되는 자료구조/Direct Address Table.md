
* 배열의 index 로 바로 접근하는 방법
	배열에서 인덱스를 순서가 아니라 key라고 생각하고 key-value 쌍을 저장하는 방식
	1: 고릴라,30 : 강아지, 509 : 고양이
	array[1] = 고릴라
	array[30] = 강아지
	array[509] = 고양이

* 장점
	* 해당 방식은 직접적으로 배열의 인덱스를 key로 사용하기 때문에 빠르게 접근이 가능하다.

* 단점 
	* 공간을 너무 많이 차지한다.
		1, 30 ,509 에 데이터가 들어갔지만 그 외에 남은 공간이 있기 때문에 공간차지가 많이 됨.

* Direct Address Table 주요 함수
	DIRECT-ADDRESS-SEARCH(T,k)
		return T[k]
	DIRECT-ADDRESS-INSERT(T,x)
		T[x.key] = x
	DIRECT-ADDRESS-DELETE(T,x)
		T[x.key] = NIL
	
	각각의 수행 시간은 O(T)   [시간 복잡도](obsidian://open?vault=TIL_yeonsang&file=TIL%2F%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0%2F%EB%B3%B5%EC%9E%A1%EB%8F%84)
	
* Direct Address Table 의 공간 복잡도
	* O([U])
	* 실제 공간 사용을 전체 공간으로 나눈 [K]/[U] 를 적재율이라고 함.
	* 적재율이 낮다면 실제로 대부분의 공간은 낭비

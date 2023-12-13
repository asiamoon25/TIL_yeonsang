
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
	
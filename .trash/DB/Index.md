## 인덱스란?

* DB 테이블에 대한 검색 성능의 속도를 높여주는 자료구조.
	특정 컬럼에 인덱스를 생성하면, 해당 컬럼의 데이터들을 정렬하여 별도의 메모리 공간에 데이터의 물리적 주소와 함께 저장됨. -> 별도의 메모리 공간에 데이터의 물리적 주소와 함께 저장.


## 자료구조

1. Hash Table
	컬럼의 값과 물리적 주소를 (key,value) 의 한쌍으로 저장하는 자료 구조.
	_잘 사용 되지 않음._ [Hash Table](obsidian://open?vault=TIL_yeonsang&file=TIL%2FDB%2FDB%EC%97%90%20%EC%82%AC%EC%9A%A9%EB%90%98%EB%8A%94%20%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0%2FHash%20Table)
2. B+Tree
	

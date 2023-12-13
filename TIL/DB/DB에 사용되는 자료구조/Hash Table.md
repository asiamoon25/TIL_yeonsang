## Hash Table 이란?
* 검색하고자 하는 키 값을 입력받아서 Hash 함수를 통해 얻은 Hash를 배열의 인덱스로 환산해서 데이터에 접근하는 자료구조
* Direct Address Table 과는 달리 Key k 가 slot h(k) 에 들어가게 됨.
	![[Pasted image 20231213170428.png]]

### h(k) 함수
* Division Method
	* 나눗셈을 이용한다. 입력값을 테이블의 크기로 나누어 계산 
		(주소 = 입력값 % 테이블의 크기)
		테이블의 크기를 소수로 정하고 2의 제곱수와 먼 값을 사용해야 효과가 좋다고 알려져 있음.
* Digit Folding
	* 각 Key 의 문자열을 ASCII 코드로 바꾸고 값을 합한 데이터를 테이블 내의 주소로 사용
* Multiplication Method
	* 숫자로 된 Key 값 K 와 0과 1 사이의 실수 A, 보통 2의 제곱수인 m 을 사용하여 계산함
		h(k) = (kAmod1) x m
		mod = % (나머지)
		kAmod1 => k x A % 1 => kA 의 소수점 이하 자리
* Universal Hashing
	* 다수의 해시 함수를 만들어 집합 H 에 넣얻두고, 무작위로 해시함수를 선택해 해시값을 만드는 기법


## 충돌

* value1 을 해시를 돌려 나온 값과 value2 를 돌려 나온 값이 동일하다면 충돌이 일어남.

### 충돌 해결법

**1. 분리 연결법**
	동일 버킷 의 데이터에 대해 자료구조를 활용해 추가 메모리를 사용하여 다음 데이터의 주소를 저장.
	Chaining 방식은 Hash Table 의 확장이 필요 없고 간단하게 구현이 가능, 삭제도 쉽다.
	데이터 수가 많아지면 chaining 데이터가 많아지며 캐시의 효율성이 감소한다.

**2. 개방주소법**
	비어있는 Hash Table 의 공간을 활용하는 방법 
	1. Linear Probing 
		Hash의 저장순서 폭을 제곱으로 저장하는 방법.
			처음 충돌이 발생한 경우에는 1만큼 그 다음 충돌 시 2^2, 3^2 칸씩 옮기는 방법
	1. Quadratic Probing: 해시

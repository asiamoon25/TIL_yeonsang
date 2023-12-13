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
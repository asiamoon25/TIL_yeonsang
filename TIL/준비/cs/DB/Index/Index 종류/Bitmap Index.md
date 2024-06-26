
## Bitmap Index 란? 

* 인덱스 컬럼의 데이터를 bit 값인 0 또는 1로 변환하여 인덱스 키로 사용함.
* 저카디널리티(적은 수의 고유한 값)를 가진 컬럼에 유용하게 적용됨.
* 각각의 컬럼 값에 대해 비트맵(이진 숫자의 배열)을 생성하고, 각 비트는 행의 존재 여부를 나타냄.

## 장단점
### 장점

1. 저장 방식 : 각 값에 대해 비트 배열이 할당되며, 특정 컬럼 값이 특정 행에 있으면 해당 비트는 1로 설정되고, 그렇지 않으면 0 으로 설정됨.

2. 효율적인 공간 사용 : 비트맵은 매우 공간 효율적이기 때문에, 작은 공간에 많은 데이터의 존재 여부를 표현할 수 있음.

3. 빠른 검색 속도 : 특정 조건에 대한 검색이나, 여러 조건의 조합(AND, OR, NOT 연산)을 통한 복합 쿼리 처리 시 매우 빠른 성능을 보임. 비트 연산은 CPU에서 매우 빠르게 처리될 수 있으므로, 적절한 상황에서 쿼리 성능이 크게 향상될 수 있음.

4. 쿼리 최적화 : 비트맵 인덱스는 복잡한 조인이나, 여러 조건의 필터링이 필요한 쿼리에서도 고성능을 유지할 수 있도록 도와줌


### 단점

1. 낮은 쓰기 성능 : DB 에서의 데이터의 추가, 삭제, 수정 작업이 빈번할 때, 비트맵 인덱스는 성능저하를 일으킬 수 있음. -> 인덱스 자체를 수정해야하기 때문

2. 고카디널리티 데이터에는 비효율적 : 많은 고유값이 있는 컬럼에 비트맵 인덱스를 사용하면, 인덱스의 크기가 커지고, 그로 인해 성능이 저하될 수 있음.


## Index 란?

* DB 테이블에 대한 검색 성능의 속도를 높여주는 자료 구조
* DB 내의 특정 컬럼(열) 이나 컬럼들의 조합에 대한 값과 해당 값이 저장된 row 의 위치를 매핑하여 DB 쿼리의 성능을 최적화 하는 데 중요한 역할을 함.


## 인덱스의 기능
1. 검색 성능 향상(조건절 where 절의 효율성)
	DB 에서 특정 데이터를 찾을 때, 인덱스를 사용하면 검색 시간을 대폭 줄일 수 있음. ➡️ 대용량 데이터에서 효과가 큼

2. 정렬된 데이터 액세스
	 인덱스는 데이터를 정렬된 상태로 저장하기 떄문에, 정렬된 순서로 데이터에 접근하고 검색하는 것이 효율적임.

3. 효율적인 데이터 집계와 범위 검색
	최대값, 최소값을 찾거나 데이터 범위를 지정하여 검색할 때 인덱스를 활용하면 처리 속도가 빨라짐.




## 인덱스 종류

1. **B-Tree 인덱스**
![[Pasted image 20240512165631.png]]

	* 가장 흔이 사용되는 인덱스 유형으로, 데이터를 균형있게 유지하는 이진 트리 구조를 가짐.
	  B-Tree 인덱스는 키 값이 정렬된 상태로 유지되어 범위 검색과 정확한 일치 검색에 적합함.
	* 숫자 및 문자열 필드에 주로 사용됨.


## 장단점

### 장점
1. 검색 대상 레코드의 범위를 줄여 검색 속도를 빠르게 할 수 있음.
2. 중복 데이터를 방지하거나 특정 컬럼의 유일성(Unique)을 보장할 수 있음.
3. ORDER BY 절과 GROUP BY 절, WHERE 절 등이 사용되는 작업이 더욱 효율적으로 처리됨.

### 단점

1. 인덱스는 추가적인 디스크 공간을 사용함.
2. 데이터가 삽입, 삭제, 업데이트 될 때마다 인덱스도 함께 갱신되어야 하므로 성능저하가 발생할 수 있음.
3. 한 페이지를 동시에 수정할 수 있는 병행성이 줄어든다.
4. 인덱스 생성 시간이 오래 걸릴 수 있음.



## 인덱스 관련 이것저것

### 인덱스 생성

1. 단일 컬럼 인덱스 생성
```sql
CREATE INDEX idx_column ON table_name (column);
```

2. 복합 컬럼 인덱스 생성
```sql
CREATE INDEX idx_compound ON table_name (column1, colum2);
```

3. 유니크 인덱스 생성
```sql
CREATE UNIQUE INDEX ide_unique_column ON table_name (column);
```

### 인덱스 삭제

```sql
DROP INDEX idx_column ON table_name;
```


### 인덱스 성능 확인

1. DB 쿼리 실행 성능 체크
(PostgreSQL, MySQL)
```sql
EXPLAIN SELECT * FROM table_name WHERE column = 'value';
```


### 인덱스 관리 및 모니터링 도구

* MySQL : `SHOW INDEX FROM table_name;` 명령어를 사용해 테이블의 인덱스 정보를 확인할 수 있음.
* PostgreSQL : `pg_indexes` 뷰를 조회하거나 `EXPLAIN` 명령어로 실행 계획을 확인할 수 있음.
* Oracle : Oracle Enterpise Manager 와 같은 GUI 도구를 사용해 인덱스 관리 및 성능 모니터링을 수행할 수 있음.
* SQL Server : SQL Server Management Studio(SSMS) 에서 인덱스 성능을 분석하고 조정할 수 있음.



### 인덱스 유지보수

DB 에 데이터가 계속 추가되고 변경되면서 인덱스의 효율성이 저하될 수 있음.

인덱스를 주기적으로 재구성하거나 재생성해야할 수 있음.

1. 인덱스 재구성(SQL Server)
```sql
ALTER INDEX ALL ON table_name REORGANIZE;
```

2. 인덱스 재생성(SQL Server)
```sql
ALTER INDEX ALL ON table_name REBUILD;
```

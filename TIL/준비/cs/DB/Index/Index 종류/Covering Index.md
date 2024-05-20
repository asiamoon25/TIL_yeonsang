
## 란?

* 특정 쿼리의 모든 필요한 데이터를 인덱스에서 직접 얻을 수 있게 하는 인덱스
  
* 인덱스를 사용하면 디스크 I/O 를 줄이고 쿼리 성능을 크게 향상 시킬 수 있음.
  
* 쿼리가 테이블의 데이터 페이지를 직접 접근하는 것을 방지하여 성능을 높여줌.


## 장단점

### 장점

1. 성능 향상 : 디스크 I/O 를 최소화 하여 쿼리 성능을 향상 시킴.

2. 데이터 페이지 접근 최소화 : 데이터 페이지에 대한 접근을 줄여 데이터베이스의 전반적인 부하를 줄임.

3. 효율적인 캐시 사용 : 인덱스는 일반적으로 메모리에 캐시 되므로 메모리 내에서 빠르게 조회할 수 있음.

### 단점

1. 인덱스 크기 증가
	* 저장 공간 
		* Covering Index 는 많은 컬럼을 포함하므로 인덱스의 크기가 커짐. 이는 더 많은 저장 공간을 필요로 하며, 특히 대용량 테이블에서 문제를 일으킬 수 있음.
		  
	* 메모리 사용
		* 큰 인덱스는 메모리에 더 많이 적재되므로 메모리 사용량이 증가함.

2. 데이터 수정 시 성능 저하
	* INSERT, UPDATE, DELETE
		* 테이블에서 데이터를 삽입, 수정, 삭제할 때마다 인덱스도 갱신되어야 함. Covering Index 는 포함된 컬럼이 많기 때문에 이 작업이 더 복잡하고 시간이 많이 걸릴 수 있음
	* 잠금(Lock) 및 병합(Merge)
		* 인덱스 갱신 시 더 많은 잠금이 필요하며, 이로 인해 동시성 문제가 발생할 수 있음.

3. 관리 복잡성 증가
	* 인덱스 설계
		* Covering Index 는 설계 시 어떤 컬럼을 포함해야 할지 신중하게 결정해야함. 잘못된 인덱스 설계는 성능 개선보다 더 많은 문제를 일으킬 수 있음.
	* 유지보수
		* 데이터베이스 스키마나 쿼리가 변경될 때 인덱스를 재설계하고 관리해야함. -> 추가적인 유지보수 작업을 필요로함.

4. 쿼리 패턴의 변화
	* 유연성 부족 
		* 특정 쿼리 패턴에 맞추어 설계된 Covering Index 는 쿼리 패턴이 변하면 더 이상 효율적이지 않을 수 있음. 새로운 쿼리에 맞추기 위해 인덱스를 다시 만들어야 할 수 있음.
		
	* 다양한 쿼리 지원 한계
		* 모든 쿼리에 대해 효율적인 Covering Index 를 설계하는 것은 불가능할 수 있으며, 일부 쿼리는 여전히 성능상의 문제를 겪을 수 있음.

5. 복잡한 인덱스 구조
	* 높은 인덱스 깊이
		* 인덱스의 키가 복잡해질수록 인덱스의 깊이가 증가할 수 있으며, 이는 인덱스 탐색 성능을 저하시킬 수 있음.
		  
	* 균형 유지
		* 인덱스 트리의 균형을 유지하는 것이 더 어려워질 수 있으며, 이는 전체적인 인덱스 성능에 영향을 미칠 수 있음.


## 예제

```sql
CREATE TABLE orders(
	order_id INT PRIMARY KEY,
	customer_id INT,
	order_date DATE,
	total_amount DECIMAL(10,2)
)
```

위와 같은 쿼리가 있다고 가정할 때

```sql
SELECT order_id, total_amount FROM orders WHERE customer_id = 123;
```

위 쿼리를 최적화 하기 위해 covering index 를 생성할 수 있음.


```sql
CREATE INDEX ind_customer_order ON orders (customer_id, order_id, total_amount);
```

 이 인덱스는 `customer_id` 로 먼저 정렬하고, 그 후에 `order_id` 와 `total_amount` 를 포함함.
이 인덱스는 `customer_id` 를 조건으로 하고, `order_id` 와 `total_amount`를 반환하는 쿼리를 완전히 커버함. 

쿼리 실행 시 테이블의 실제 데이터 페이지에 접근 할 필요 없이 인덱스만으로 결과를 반환할 수 있음.



## Index Included Columns(인덱스 포함 컬럼)

일부 DB 는 인덱스의 INCLUDE 기능을 제공함.

이러한 Include 는 인덱스 트리의 리프 페이지에만 저장되며, 인덱스의 키의 일부로 간주되지 않음.

예를 들어서 위의 예제에서 `order_date` 는 쿼리 조건에는 사용되지 않지만 반환될 수 있는 컬럼임.
```sql
CREATE INDEX idx_customer_order_include ON orders (customer_id) INCLUDE (order_id, total_amount, order_date);
```

이러한 인덱스를 사용하면 쿼리는 covering index 효과를 보면서 인덱스 키의 크기를 줄일 수 있음.


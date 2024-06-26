---
sticker: emoji//1f468-200d-1f373
---
## 란?

* PostgreSQL 과 같은 Database 시스템에서 다양한 사용자 정의 데이터 타입과 쿼리를 효율적으로 지원하기 위해 설계된 인덱스 구조임.
  
* GiST 는 균형 트리 구조를 가지며, B-Tree 와 유사하지만 더 유연한 데이터 분배 및 접근 방법을 제공함.
  


## GiST 와 B-Tree 차이점

* B-Tree 인덱스
	* 비교 연산자(크다, 작다, 같다)에 엄격하게 연결되어 있음.이러한 연산자는 숫자나 문자열 데이터 타입에는 유용하지만, 지리 데이터, 텍스트 문서, 이미지와 같은 데이터 타입에는 적합하지 않음.
* GiST Index
	* 임의의 데이터 타입을 균형 트리에 분배하는 규칙을 정의하고, 이를 이용해 특정 연산자로 데이터를 접근할 수 있는 방법을 제공함.
	* GiST 인덱스는 공간 데이터에 대한 상대 위치 연산자(왼쪽에 있다, 오른쪽에 있다, 포함한다 등)을 지원하는 R-Tree 를 수용할 수 있음.

## GiST 의 확장성

PostgreSQL 에서 완전히 새로운 인덱스 메소드를 만들려면, 인덱스 엔진과의 인터페이스를 구현해야함.

인덱싱 논리뿐만 아니라 데이터 구조를 페이지에 매핑하는 방법, 효율적인 잠금 구현, 그리고 Write-Ahead Log 지원 등 복잡한 작업을 포함함.

GiST 는 이러한 저수준 문제를 해결하고, 응용 도메인에 맞는 여러 함수를 제공하여 새로운 접근 방법을 쉽게 구축할 수 있는 프레임워크 역할을 함.



## 구조
Gist 는 높이 균형 트리로, 노드 페이지로 구성됨.
각 노드는 인덱스 행으로 구성됨.

* 리프 노드의 각 행(리프 행)
	* 일반적으로 어떤 조건(predicate) 과 테이블 행(TID)에 대한 참조를 포함함.

* 내부 노드의 각 행(내부 행)
	* 조건과 자식 노드에 대한 참조를 포함하며, 자식 서브트리의 모든 인덱스 데이터는 이 조건을 만족해야함.


## 검색

GiST 트리에서 검색은 "일관성 함수(consistent)" 를 사용함. 이 함수는 인덱스 행의 조건이 검색 조건과 일치하는지 판단함.

루트 노드에서 검색이 시작되며, 일관성 함수는 하위 노드로 내려갈지 여부를 결정함.

검색은 깊이 우선 탐색으로 수행되며, 가능한 한 빨리 리프 노드에 도달하여 결과를 반환함.

**ex) R-Tree**
지리 데이터의 경우, R-Tree 는 평면을 직사각형으로 나누어 모든 포인트를 포함하도록 함. 인덱스 행은 직사각형을 저장하며, 조건은 `포인트가 주어진 직사각형 내에 있다` 와 같은 형태가 됨. 예를 들어 `points` 테이블에 포인트 데이터를 저장하고 GiST 인덱스를 생성할 수 있음.

```sql
CREATE TABLE points(p points);

INSERT INTO points(p) VALUES
	(point '(1,1)'), (pont '(3,2)'), (point '(6,3)'),
	(point '(5,5)'), (point '(7,8)'), (point '(8,6)');
CREATE INDEX ON points USING gist(p);
```

이 인덱스를 사용하여 특정 직사각형 내에 있는 모든 포인트를 찾는 쿼리를 수행할 수 있음.

```sql
SELECT * FROM points WHERE p <@ box '(2,1),(7,4)';
```

**ex) 내부구조 분석**
`gevel` 확장을 사용하여 GiST 인덱스의 내부 구조를 분석할 수 있음. 예를 들어, 인덱스 트리의 통계를 확인할 수 있음.
```sql
SELECT * FROM gist_stat('points_p_idx');
```


**ed) 시간 간격 및 배타 제약 조건**

GiST 는 시간간격(`tsrange` 타입) 및 배타 제약조건(`EXCLUDE`) 를 지원함.
예를 들어, 예약 시스템에서 교차하는 시간 간격을 허용하지 않는 제약 조건을 추가할 수 있음.

```sql
CREATE TABLE reservations(during tsrange);
INSERT INTO reservations(during) VALUES 
  ('[2016-12-30, 2017-01-09)'), 
  ('[2017-02-23, 2017-02-27)'), 
  ('[2017-04-29, 2017-05-02)');
CREATE INDEX ON reservations USING gist(during);
ALTER TABLE reservations ADD EXCLUDE USING gist(during WITH &&);
```

교차하는 시간 간격을 삽입하려고 하면 오류 발생

```sql
INSERT INTO reservations(during) VALUES ('[2017-05-15, 2017-06-15)');
```


## 연산자

* **공간 데이터 (Geometry)**

|연산자|설명|예시|
|---|---|---|
|`@>`|포함 (contains)|`geom @> other_geom`|
|`<@`|포함됨 (contained by)|`geom <@ other_geom`|
|`&&`|겹침 (overlaps)|`geom && other_geom`|
|`<<`|좌측에 있음 (is left of)|`geom << other_geom`|
|`>>`|우측에 있음 (is right of)|`geom >> other_geom`|
|`&<`|우측 경계와 겹치지 않음 (does not extend to the right of)|`geom &< other_geom`|
|`&>`|좌측 경계와 겹치지 않음 (does not extend to the left of)|`geom &> other_geom`|
|`<<|`|아래에 있음 (is below)|
|`|>>`|위에 있음 (is above)|
|`&<|`|위쪽 경계와 겹치지 않음 (does not extend upwards)|
|`|&>`|아래쪽 경계와 겹치지 않음 (does not extend downwards)|

* **범위 데이터(Range)**

| 연산자  | 설명                                              | 예시                 |
| ---- | ----------------------------------------------- | ------------------ |
| `@>` | 포함 (contains)                                   | `range @> value`   |
| `<@` | 포함됨 (contained by)                              | `value <@ range`   |
| `&&` | 겹침 (overlaps)                                   | `range1 && range2` |
| `<<` | 좌측에 있음 (is left of)                             | `range1 << range2` |
| `>>` | 우측에 있음 (is right of)                            | `range1 >> range2` |
| `&<` | 우측 경계와 겹치지 않음 (does not extend to the right of) | `range1 &< range2` |
| `&>` | 좌측 경계와 겹치지 않음 (does not extend to the left of)  | `range1 &> range2` |
| `-   | -`                                              | 인접함 (adjacent to)  |
| `=`  | 같음 (equals)                                     | `range1 = range2`  |

* **텍스트 데이터(Full-text Search)**

|연산자|설명|예시|
|---|---|---|
|`@@`|매치 (match)|`tsvector @@ tsquery`|

* **IP 주소 데이터**

| 연산자   | 설명                                              | 예시                |
| ----- | ----------------------------------------------- | ----------------- |
| `<<`  | 서브넷에 포함 (contained by subnet)                   | `inet << subnet`  |
| `<<=` | 서브넷에 포함되거나 같음 (contained by or equal to subnet) | `inet <<= subnet` |
| `>>`  | 서브넷 포함 (contains subnet)                        | `inet >> subnet`  |
| `>>=` | 서브넷 포함하거나 같음 (contains or equal to subnet)      | `inet >>= subnet` |
| `&&`  | 겹침 (overlaps)                                   | `inet && subnet`  |

**예시**

* 공간데이터 
```sql
-- 포인트 데이터에 대한 GiST 인덱스 생성
CREATE TABLE points(p point);
INSERT INTO points(p) VALUES 
  (point '(1,1)'), (point '(3,2)'), (point '(6,3)'), 
  (point '(5,5)'), (point '(7,8)'), (point '(8,6)');
CREATE INDEX ON points USING gist(p);

-- 특정 박스 내에 포함된 포인트 검색
SELECT * FROM points WHERE p <@ box '(2,1),(7,4)';

```

* 범위 데이터

```sql
-- 범위 데이터에 대한 GiST 인덱스 생성
CREATE TABLE reservations(during tsrange);
INSERT INTO reservations(during) VALUES 
  ('[2016-12-30, 2017-01-09)'), 
  ('[2017-02-23, 2017-02-27)'), 
  ('[2017-04-29, 2017-05-02)');
CREATE INDEX ON reservations USING gist(during);

-- 특정 범위와 겹치는 예약 검색
SELECT * FROM reservations WHERE during && '[2017-01-01, 2017-04-01)';

```

* 풀 텍스트 검색
```sql
-- 텍스트 데이터에 대한 GiST 인덱스 생성
CREATE TABLE documents(doc text, doc_tsv tsvector);
INSERT INTO documents(doc) VALUES 
  ('Can a sheet slitter slit sheets?'), 
  ('How many sheets could a sheet slitter slit?');
UPDATE documents SET doc_tsv = to_tsvector(doc);
CREATE INDEX ON documents USING gist(doc_tsv);

-- 특정 텍스트와 매치되는 문서 검색
SELECT * FROM documents WHERE doc_tsv @@ to_tsquery('sheet & slitter');
```

* IP 주소 데이터
```sql
-- IP 주소 데이터에 대한 GiST 인덱스 생성
CREATE TABLE networks(ip inet);
INSERT INTO networks(ip) VALUES 
  ('192.168.1.0/24'), 
  ('10.0.0.0/8'), 
  ('172.16.0.0/12');
CREATE INDEX ON networks USING gist(ip);

-- 특정 IP 주소와 겹치는 네트워크 검색
SELECT * FROM networks WHERE ip && '192.168.1.128/25';

```
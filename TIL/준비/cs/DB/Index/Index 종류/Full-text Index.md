
## 란?

* 많은 형태의 데이터가 있을 때 효율적으로 데이터를 찾는 방법 중 하나 텍스트로 구성된 데이터의 내용을 가지고 생성한 인덱스
* 대량의 텍스트를 데이터를 포함하는 컬럼에서 검색을 최적화 하는 데 유용함.
* 단순 문자열 비교를 넘어서, 텍스트의 의미와 형태를 고려한 검색이 가능함.


## 주요 개념

1. Tokenization(토큰화)
	* 텍스트 데이터를 단어, 문장 또는 토큰으로 분리하는 과정
	ex) "The quick brown fox" 라는 문장은 "The", "quick","brown","fox" 로 분리됨.

2. 스테밍(Stemming) 및 표제어 추출(Lemmatization)
	* 단어의 변형된 형태를 동일한 기본 형태로 통합하는 과정.
	ex) "running", "runs", "ran" 은 모두 "run" 으로 처리됨.

3. 정규화
	* 텍스트 데이터를 소문자로 변환하거나 불필요한 구두점 등을 제거하는 과정을 포함. ➡️ 일관된 검색 결과를 위해 필요함.

4. 인버티드 인덱스(Inverted Index)
	* 각 단어가 출현하는 위치를 저장한 인덱스
	ex) "fox" 가 문서 1의 3번째 단어이고, 문서 2의 5번째 단어인 경우, 인버티드 인덱스는 "fox:{1:3, 2:5}" 와 같이 저장됨.


## 기능

1. 단어 검색
	* 특정 단어나 구문을 포함하는 문서를 빠르게 찾을 수 있음..

2. Boolean 검색
	* AND, OR, NOT 등의 논리 연산자를 사용하여 복합적인 검색 조건을 처리할 수 있음.

3. 프레이즈 검색(Pharase Search)
	* 정확한 구문을 포함하는 문서를 검색함.
	ex) "quick brown fox" 라는 구문을 찾음.

4. 가중치 기반 검색
	* 단어의 중요도에 따라 검색 결과의 순위를 매김. 예를 들어, 검색어와 문서 간의 유사도를 계산하여 순위를 매김.

5. 근접 검색(Proximity Search)
	* 두 단어가 문서 내에서 서로 얼마나 가까운지에 따라 검색 결과를 조정할 수 있음.


## 사용 예

MySQL 에서의 풀텍스트 인덱스 사용

1. 테이블 생성 및 풀텍스트 인덱스 추가
```sql
CREATE TABLE articles(
	id INT AUTO_INCREAMENT PRIMARY KEY,
	title VARCHAR(255),
	body TEXT,
	FULLTEXT(title, body)
)
```

2. 데이터 삽입
```sql
INSERT INTO articles (title, body) VALUES
('MySQL Full-Text Search', 'This is an article about MySQL full-text search.'),
('Full-Text Search in Databases', 'Full-text search is essential for searching large text data.'),
('Introduction to Databases', 'This article introduces the basics of databases.');
```

3. 풀 텍스트 검색
```sql
SELECT * FROM  articles
WHERE MATCH(title, body) AGAINST('full-text search');
```


PostgreSQL 에서의 풀텍스트 인덱스 사용

1. 테이블 생성
```sql
CREATE TABLE documents (
    id SERIAL PRIMARY KEY,
    content TEXT
);
```
2. 데이터 삽입
```sql
INSERT INTO documents (content) VALUES
('This is an article about PostgreSQL full-text search.'),
('Full-text search is essential for searching large text data in databases.'),
('This article introduces the basics of databases.');
```

3. 풀텍스트 인덱스 생성
```sql
CREATE INDEX idx_fts_content ON documents USING gin(to_tsvector('english', content));
```

4. 풀텍스트 검색
```sql
SELECT * FROM documents
WHERE to_tsvector('english', content) @@ to_tsquery('full-text & search');
```



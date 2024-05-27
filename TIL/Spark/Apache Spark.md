# Spark 란?

* 빅데이터 처리를 위한 오픈소스 분산 처리 플랫폼.
* 빅데이터 분산 처리 엔진

## 주요 기능
* Batch / Streaming data
	데이터를 batch 처리 또는 실시간 처리할 수 있음.
	SQL,Python, Scala, Java, R 과 같은 Spark 에서 지원하는 언어를 사용할 수 있음.
	고수준의 Stream 처리 기능을 제공하는 구조적 스트리밍(Structured Streaming) 라이브러리를 제공

* SQL Analytics
	빠른 분산 SQL Query 를 지원함.
		Spark SQL 을 사용하면 기존에 DB 서비스에 SQL Query 를 실행 시키는 방식과 비슷한 SQL 문법으로 Query를 실행 시킬 수 있음.

* Data science at scale
	petabyte 같은 큰 데이터에 대해서도 EDA(탐색적 데이터 분석) 을 수행할 수 있음.
		_EDA_ : 데이터를 조회하면서 패턴, 특이성과 같은 인사이트를 지속적으로 탐색하는 과정

* Machine learning
	다양한 머신러닌(ML) 알고리즘 라이브러리를 지원하며, 많은 연산을 필요로 하는 훈련을 클러스터의 여러 Machine 을 활용하여 수행할 수 있음.

## Spark EcoSystem
![[Pasted image 20231127180541.png]]

* Apache Spark Core
	스파크가 제공하는 모든 기능은 Spark Core 위에 구축되어 있음.
	스파크 코어는 인메모리 연산 기능을 제공하여 빠른 속도를 제공함.
	Spark Core는 대규모 데이터 세트의 병렬 및 분산 처리의 기반이됨.
	* 주요기능 
		* 필수 입출력 기능담당
		* Spark Cluster의 역할을 프로그래밍하고 관찰함
		* 작업 디스패치
		* 장애 복구
		* In-Memory 를 사용하여 MapReduce의 문제점을 극복
	Spark Core 에서는 RDD 라는 특수 컬렉션이 포함되어 있음.([작성한 글](obsidian://open?vault=TIL_yeonsang&file=TIL%2FSpark%2FRDD))

Apache Spark SQL
	정형 데이터 처리를 위한 스파크 모듈. RDD API 와 다르게, Spark SQL 인터페이스는 데이터와 수행되는 컴퓨팅과 관련한 구조에 대한 정보를 제공함.
	Spark SQL 은 2가지 주요 기능을 가지고 있음.
		1. Spark SQL Programming Interface
			Spark Core 에 기반한 라이브러리 형태로 실행됨. Spark SQL 인터페이스를 제공.
			JDBCC/ODBC , CommandLine Console, Spark 가 지원하는 언어의 DataFrame API 3가지를 통해 접근할 수 있음.
				1. DataFrame API
					동일한 스키마를 가진 rows 들의 분산 콜렉션
				2. 데이터프레임 연산
					DSL 를 통해 데이터프레임 연산을 수행할 수 있음.
					projection(select), filter(where), join, aggregations(group By) 와 같은 일반적인 관계형 연산을 모두 지원.
					이러한 연산자는 limited DSL 상의 expression 객체를 취하여 Spark 가 expression의 구조를 감지하도록 함.
				3. 데이터프레임 vs 관계형 쿼리 언어
					Spark SQL 은 절차형 및 관계형 인터페이스를 통합하여 제공하기에 사용자가 매우 편리하게 작업을 진행할 수 있도록 함.
					사용자는 Scala,Java, Python 으로 된 함수로 데이터프레임을 전달하여 논리적 플랜을 만들고, 최종적으로 전체 플랜에 있어 최적화의 이점도 누릴 수 있음.
				4. In-Memory Caching
					Spark SQL 은 이전의 Shark 와 같이 자주 사용되는 데이터를 컬럼형 스토리지를 사용해 메모리에 materilize(cache) 할 수 있음. Spark 의 Native 캐시는 데이터를 단순히 JVM 객체로 저장하는 반면에, 컬럼형 캐시는 dictionary encoding 과 run-length 인코딩과 같은 컬럼 압축 방식을 적용하기에 메모리 소비량이 매우 적습니다.
				5. User-Defined Functions
		2. Catalyst Optimizer
			쿼리 최적화 도구
			Scala의 함수형 프로그래밍 constructs 에 기반하여 2가지 목적을 위해 디자인 되었음.
			1. Spark SQL 에 새로운 최적화 테크닉과 기능을 쉽게 더할 수 있도록
			2. 외부 개발자가 옵티마이저를 확장할 수 있도록.
		3. 트리
			Catalyst의 메인 데이터 타입은 node 객체로 구성된 tree 임.
			각 노드는 노드 타입과 0개 또는 그 이상의 children 을 가짐. 새로운 node 타입은 Scala 에서 TreeNode 클래스의 서브타입으로 정의되게 됨. 이러한 객체들은 immutable 하고 이후에 나올 함수형 transformation을 통해 조작될 수 있음.
		4. Rules
			하나의 트리에서 다른 트리로의 함수.
			rule 이 input 트리에 대해 임의적인 코드를 실행할 수 있지만, 가장 일반적인 접근은 패턴매칭 세트를 사용하여 서브트리의 일부분을 찾고 특정 구조로 바꾸는 것임.



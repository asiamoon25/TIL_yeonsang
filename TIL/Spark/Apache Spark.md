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

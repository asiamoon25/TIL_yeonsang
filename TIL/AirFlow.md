apache airflow

### 워크플로우 오픈소스 플랫폼
* 워크플로우란?
	의존성으로 연결된 작업(Task) 들의 집합
	ETL 의 경우 Extarction > Transformation > Loading 의 작업 흐름


### 구성 및 작동 원리

구성
	1. 워크플로우 정의(DAGs)
		워크 플로우를 정의하는 핵심 구성 요소
		DAGs 는 여러 개의 작업(Task)과 이 작업들 간의 의존성을 정의
		Python 언어를 사용하여 DAGs 를 정의
	2. 작업(Tasks)
		작업은 DAG의 기본 구성 단위로, 워크플로우에서 실행되는 개별적인 작업을 나타냄.
		airflow 에는 다양한 유형의 작업을 지원하는 'Operator' 가 내장되어 있음.
			-> BashOperator, PythonOperator, EmailOperator
	3. 스케줄러
		스케줄러는 DAG 를 모니터링 하고, 스케줄에 따라 작업을 실행함.
		정의된 스케줄에 따라 DAG를 실행하며, 작업의 의존성을 관리
	4. 웹 서버
		airflow의 사용자 인터페이스를 제공
		웹 브라우저를 통해 DAG의 상태를 모니터링하고, 워크플로우를 관리 할 수 있음.
	5. 메타데이터 데이터베이스
		airflow 의 상태, DAG 의 구성 및 작업의 로그 정보 등을 저장함.
		postgreSQL, MySQL 등 다양한 데이터베이스를 사용할 수 있음.


#### 스케줄러
**apache scheduler** 임.

1. 작업 스케줄링
	스케줄러는 정의된 DAGs를 주기적으로 확인하고 스케줄에 따라 작업(Task)를 실행함.
	
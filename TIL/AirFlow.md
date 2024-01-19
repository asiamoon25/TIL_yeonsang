apache airflow

### 워크플로우 오픈소스 플랫폼
* 워크플로우란?
	의존성으로 연결된 작업(Task) 들의 집합
	ETL 의 경우 Extarction > Transformation > Loading 의 작업 흐름


### 구성 및 작동 원리
1) Airflow Key Concept
	단어 뜻 그대로 순환하지 않는 그래프, DAG 라고 부름
	반복이나 순환을 허용하지 않음
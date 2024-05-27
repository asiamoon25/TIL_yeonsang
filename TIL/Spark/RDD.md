# RDD
* ***Resilient Distributed Data**
	1. 탄력적인 분산 데이터 셋
	2. Spark 가 사용하는 핵심 데이터 모델, 다수의 서버에 걸쳐 분산 방식으로 저장된 요소들의 집합, 병렬 처리가 가능하며 장애가 발생할 경우 스스로 복구될 수 있는 내성을 가지고 있음.
	3. 내부에는 단위 데이터를 포함하고 있고 저장할 때는 여러 서버에 나누어 저장되며, 처리할 때는 각 서버에 저장된 데이터를 동시에 병렬로 처리할 수 있는 모델

* 특징
	1. 데이터 추상화
		데이터는 클러스터에 흩어져 있지만 하나의 파일인 것 처럼 사용이 가능하다.
		여러 곳에 데이터를 객체 하나에 담을 수 있음.
	
	2. 탄력적 & 불변성 (Resilient & Immutable)
		데이터는 탄력적이고 불변(Resilient & Immutable) 하는 성질이 있다.
		만약 데이터가 네트워크 장애나 하드웨어, 메모리 문제, 알 수 없는 갖가지 이유로 연산 중 여러 노드 중 하나가 망가진다면, 데이터가 불변(Immutable) 하면 문제가 일어날 때 복원이 가능해진다.
	
	3. 타입 세이프
		RDD 는 컴파일 시 타입을 판별할 수 있어 문제를 일찍 발견할 수 있기 때문에 개발자 친화적이다.
	
	4. 정형 & 비정형 데이터
		정형 / 비정형 데이터(Unstructured/Structured Data) 를 모두 담을 수 있다.
	
	5. Lazy
		RDD 는 연산이 필요할 때까지 연산을 하지 않는다.
		액션(A, Action) 을 할 때 까지 변환(T, Transformation)은 실행되지 않는다.
			스파크 오퍼레이션 = 변환 + 액션
		RDD3 에서 RDD4로의 액션이 일어나기 전까지 RDD1 -> RDD3 까지의 변환을 실행하지 않는다. => 게으른 연산(Lazy Evaluation)
		Action 이 실행됐을 때만 생성된 계보를 생성.
	
	6. 다수의 파티션으로 관리됨
		* 하나의 RDD 는 여러 파티션으로 나뉨.
		* 파티션의 개수, 파티셔너(Hash,Range) 등을 선택 가능하다.




* ***Lineage(계보)**
	![[Pasted image 20231124140736.png]]
	어떻게 RDD 연산이 처리될 것인지를 기록
	RDD 는 불변하는 특성으로 인해 기존에 있던 RDD를 활용하는 것이 아닌 새로운 RDD 를 생성하게됨 -> 이 때 생성되는 연산 순서가 바로 Lineage
	
	* 특징
		1. Lineage 는 DAG 형태로 되있음.
			![[Pasted image 20231124140043.png]]
		2. 노드 간의 순환이 없고, 일정한 방향성을 가짐.
			DAG 형태이기 때문에 장애 발생 시 그래프를 다시 복기하여 다시 계산하고, 자동으로 복구 할 수 있음.

* Operation
	* Transformation
		* 기존의 RDD를 변경하여 새로운 RDD 를 생성
		-> return 이 RDD가 됨.
	
	* Action
		* RDD 값을 기반으로 계산하여 결과를 생성하는 것
		-> return 값이 데이터 또는 실행 결과
		* collect, count, top, reduce 등

*  RDD 동작 원리 핵심
	* Lazy Evaluation(느긋한 연산)
		* task 를 정의할 때는 연산을 하지 않다가 결과가 필요할 때 연산하는 것을 말함.
			즉, RDD 는 Action 연산자를 만나기 전까지는, Transformation 연산자가 아무리 쌓여도 처리하지 않음.

* DAG (Directed Acyclic Graph)
	* RDD 를 변형하는 순서를 Lineage 라고 하며, Lineage 는 DAG(Directed Acylic Graph) 의 형태를 가짐.
	* DAG 의 형태
		![[Pasted image 20231124140043.png]]
		node 간의 순환이 없으며, 일정한 방향성을 가지기 때문에 각 노드간에는 의존성이 있고, 노드간의 순서가 중요함.
		따라서 RDD 연산과정에서 특정 RDD 관련 정보가 **메모리에서 유실됐을 경우**, DAG 그래프를 복기하여 다시 계산하고 복구할 수 있음.
		Spark 는 이러한 특성 때문에 Fault-tolerant(장애 허용)을 잘 보장함.



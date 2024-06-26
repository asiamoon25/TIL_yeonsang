## 란?
* 대규모 데이터를 효율적으로 관리하기 위해 데이터베이스를 여러 개의 작은 조각(샤드)으로 분할하는 방식
* 각 샤드가 독립적인 데이터베이스 인스턴스로 작동함.


## 주요 유형

1. 범위 기반 샤딩(Range-based Sharding)
	* 범위 기반 샤딩은 샤딩 키의 값에 따라 데이터를 범위별로 분할하는 방법.
	* 이 방식은 샤딩 키(예: 사용자 ID, 날씨 등)에 따라 샤드가 처리하는 데이터의 범위를 명확히 정의함.
	* 장점 
		* 범위 쿼리(예 : 특정 ID 범위의 사용자 찾기)에 유리함.
		* 데이터가 어느 샤드에 있는지 예측하기 쉬움.
	* 단점
		* 데이터 분포가 불균형할 수 있어, 일부 샤드에 과부하가 걸릴 가능성이 있음.
		* 시간이 지남에 따라 데이터의 불균형을 해결하기 위한 재샤딩이 필요할 수 있음 

2. 해시 기반 샤딩(Hash-based Sharding)
	* 해시 기반 샤딩은 샤딩 키에 해시 함수를 적용하여 데이터를 분할함. 해시 함수의 결과 값을 기반으로 데이터를 샤드에 할당하기 때문에 데이터가 샤드에 보다 균등하게 분포될 수 있음.
	* 장점
		* 데이터가 균등하게 분포되어 각 샤드의 부하를 평등하게 유지할 수 있음.
		* 데이터 스케일 아웃이 쉽고 관리가 편리함.
	* 단점
		* 해시 충돌이 발생할 수 있으며, 범위 쿼리 성능이 저하될 수 있음.
		* 해시 함수의 선택이 성능에 큰 영향을 미침.

3. 리스트 기반 샤딩(List-based Sharding)
	* 리스트 기반 샤딩은 데이터를 특정 값의 목록에 따라 분할함. 각 샤드는 명확하게 정의된 값의 리스트를 기반으로 데이터를 저장함.
	* 장점 
		* 명확하게 정의된 규칙에 따라 데이터를 분할할 수 있어 관리가 용이함.
		* 특정 쿼리 유형(예: 특정 국가의 사용자)에 최적화 할 수 있음.
	* 단점
		* 목록을 재정의하고 데이터를 재분배해야 하는 경우 관리가 복잡해질 수 있음.
		* 데이터 분포가 시간에 따라 변경될 수 있어 샤드 간 부하 불균형이 발생할 수 있음.

4. 지리 기반 샤딩(Geographic Sharding)
	* 지리 기반 샤딩은 데이터를 지리적 위치에 따라 분할 함. 이 방식은 사용자의 위치에 따라 데이터를 가까운 데이터 센터의 샤드에 저장하여 응답시간을 개선할 수 있음.
	* 장점
		* 지역별 데이터 규제 준수에 유리함.
		* 사용자에게 더 빠른 데이터 접근 속도를 제공할 수 있음.
	* 단점
		* 지리적 분할을 위한 추가 인프라와 복잡한 데이터 관리가 필요함.
		* 특정 지역의 데이터가 과부하 될 수 있음.


## 고려사항
* 데이터 분포 : 데이터가 샤드에 균등하게 분포되어 있는지 확인해야함.
  
* 쿼리 패턴 : 애플리케이션의 쿼리 패턴을 분석하여 가장 효율적인 샤딩 전략을 선택해야함.
  
* 관리 복잡성 : 샤딩 전략이 시스템의 관리 복잡성을 증가시키지 않도록 해야함.

샤딩은 데이터베이스 설계와 운영에 큰 영향을 미치므로, 샤딩 전략을 선택할 때는 데이터의 특성, 애플리케이션 요구 사항, 시스템의 확장성 요구 등을 면밀히 고려해야 함.
![[Pasted image 20240521141513.png]]

## CAP 이론

일관성(Consistency), 가용성(Availability), 분할 내성(Partition tolerance) 의 약자 이며, 이 세 가지 속성 중에서 동시에 모두를 만족시킬 수 없다는 이론

* 일관성(Consistency)
	* 데이터를 저장하는 장비가 1대 또는 100대 이던지 간에 모든 장비에서 동일한 데이터가 저장되어 있어야 한다는 것. ACID 원리에서 의미하는 것과 같음.
	  어떤 DB 속성에 c가 있다면, 트랜잭션 기능 또는 그와 비슷한 매커니즘이 존재한다는 뜻.

* 가용성(Avai)
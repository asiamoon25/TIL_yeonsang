
## 란? 

`ConcurrentHashMap` 은 Java 의 Collection Framework 에서 멀티 스레드 환경에서 안전하게 사용할 수 있는 고성능의 Map의 구현체임.
`HashMap` 과 유사하지만, 동시성을 제공하여 여러 스레드가 동시에 안전하게 데이터를 읽고 쓸 수 있게 설계되었음.

## 원리

`ConcurrentHashMap` 은 내부적으로 다양한 최적화 기법을 사용하여 동시성을 관리함.

1. **Segment Locks**
	* Java 7 까지는 `ConcurrentHashMap` 이 여러 개의 세그먼트로 나누어져 각 세그먼트에 별도의 락을 적용함.
	* Java 8 이후에는 더 세분화된 버킷 단위로 락을 적용하여 동시성을 더욱 향상 시켰음.

2. **CAS(Compare-And-Swap) 연산**
	* 원자적 연산을 위해 CAS 연산을 사용함. 이는 락을 걸지 않고도 안전하게 값을 변경할 수 있도록 함.
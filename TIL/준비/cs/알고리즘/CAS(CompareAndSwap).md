
## 란?

CAS(Compare-And-Swap) 는 동시성 제어 메커니즘으로, 락을 사용하지 않고도 변수의 값을 원자적으로 업데이트할 수 있는 알고리즘임.

CAS 는 주로 멀티스레드 환경에서 안전한 비동기적 프로그래밍을 위해 사용됨.

## 작동

* CAS 는 세 가지 값(메모리 위치, 예상 값, 새로운 값) 을 사용하여 작동함.
	1. **메모리 위치**
		* 변경하고자 하는 변수의 메모리 주소
* 2. **예상 값**
	* 현재 예상하는 변수의 값
3. **새로운 값**
	* 변수에 설정하려는 새 값

**작동방식**
* 메모리 위치에 저장된 현재 값이 예상 값과 같은지 비교함.
* 예상 값과 현재 값이 같으면, 새로운 값으로 변경함.
* 예상 값과 현재 값이 다르면 아무 작업도 하지 않고 종료함.

이 과정은 원자적으로 이루어지며, 여러 스레드가 동시에 이 연산을 시도해도 항상 일관된 결과를 보장함.


## CAS 동작 방식

CAS 알고리즘은 하드웨어 수준에서 지원되며, 일반적으로 다음과 같은 단계를 거침.

1. **비교**
	* 메모리 위치의 현재 값을 예상 값과 비교함.
2. **교체**
	* 현재 값이 예상 값과 같다면, 새로운 값으로 교체함. 그렇지 않으면 아무런 변화도 하지 않음.
3. **반복**
	* 예상 값과 현재 값이 다를 경우, 다시 시도함. 이 과정은 성공할 때까지 반복됨.



## CAS 사용법

JAVA 에서 CAS 는 주로 `java.util.concurrent.atomic` 패키지에서 제공하는 클래스들을 통해 사용됨. 대포적인 클래스는 `AtomicInteger`, `AtomicLong`, `AtomicReference` 등이 있음.

**AtomicInteger**

```java
public class CASExample{
	public static void main(String[] args) {
		AtomicInteger atomicInteger = new AtomicInteger(0);
		
		int expectedValue = 0;
		int newValue = 1;
		
		//Compare and Swap
		boolean wasUpdated = atomicInteger.compareAndSet(expectedValue, newValue);
		
		if(wasUpdated) {
			System.out.prinln("Update successful: " + atomicInteger.get());
		}else{
			System.out.println("Update failed: " + atomicInteger.get());
		}
	}
}
```

`compareAndSet` 메서드를 사용하여 현재 값이 예상 값과 같을 경우 새로운 값으로 교체함.


### CAS 내부 동작

`compareAndSet` 메서드는 JVM 내에서 원자적 연산을 보장하는 하드웨어 명령어를 사용하여 구현 됨. 이러한 명령어는 CPU 가 제공하며, 일반적으로 다음과 같은 순서로 작동함.


1. `compareAndSet` 메서드는 CPU 의 CAS 명령어를 호출함.
2. CPU 는 지정된 메모리의 주소의 값을 읽고, 예상 값과 비교함.
3. 예상 값과 현재 값이 같으면 , CPU는 새로운 값을 메모리 주소에 저장함.
4. 예상 값과 현재 값이 다르면, 아무 작업도 하지 않고 false 를 반환함.
5. 메서드는 true 또는 false 를 반환하여 연산이 성공했는지 여부를 나타냄.


## CAS 의 장단점

**장점**
* **락 프리 동기화**
	* 락을 사용하지 않으므로 교착 상태(데드락)가 발생하지 않음.
* **고성능**
	* 락을 사용한 동기화보다 성능이 우수함. 특히, 스레드 경합이 적은 경우에 효과적임.

**단점**
* **반복 시도 비용**
	* 예상 값과 현재 값이 다를 경우 반복적으로 연산을 시도해야 하므로, 경합이 심한 환경에서는 성능이 저하될 수 있음.
* **복잡성**
	* 일반적인 락 기반 동기화보다 이해하고 구현하기 어려울 수 있음.

## CAS 적용

* **원자적 변수 업데이트**
	* 멀티스레드 환경에서 안전하게 변수 값을 업데이트할 때 사용됨.
* **비차단 알고리즘**
	* 락을 사용하지 않는 비차단 알고리즘(Non-blocking Algorithms) 을 구현때 핵심적으로 사용됨.
* **Concurrent Collections**
	* Java 의 `ConcurrentHashMap`, `ConcurrentHashMap`

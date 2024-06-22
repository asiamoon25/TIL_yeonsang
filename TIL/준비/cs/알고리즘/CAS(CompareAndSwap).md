
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
			System.out.prinln("Update successful: " + atomicInteger.get())
		}
	}
}
```
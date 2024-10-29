

## 차이점


1. **ConcurrentHashMap**
	* **동시성 제어**
		* 높은 동시성을 제공하며, 여러 스레드가 동시에 접근할 수 있도록 설계되어있음. 전체 맵에 락을 걸지 않고, 버킷 단위로 락을 걸어 성능을 향상시킴.
	* **null 키와 값**
		* Null 키와 값을 허용하지 않음.
	* **동기화 메커니즘**
		* 세그먼트 락 또는 버킷 락을 사용하여 동시성을 제어함.

2. **Hashtable**
	* **동시성 제어**
		* 모든 메서드가 동기화되어 있으며, 멀티스레드 환경에서 안전하지만 성능이 저하됨.
	* **null key 와 값**
		* Null 키와 값을 허용하지 않음.
	* **동기화 메커니즘**
		* 모든 메서드에 synchronized 키워드를 사용하여 동기화를 제공함.


## 각 특징

1. ConcurrentHashMap
	* **멀티스레드 환경** 에서 높은 성능 제공
	* **버킷 단위 락**으로 인해 병렬성이 뛰어남.
	* Null 키와 값을 허용하지 않음.
	* Java 5 부터 도입됨.
	* 원자적 연산을 지원(`putIfAbsent`, `replace` 등)

2. HashMap
	* **단일 스레드 환경** 에서 빠른 성능 제공
	* 동기화가 필요 없는 경우에 적합
	* Null 키와 값을 허용
	* Java 1.2 부터 도입됨.
	* 동기화 되지 않음.

3. Hashtable
	* **동기화된 메서드** 제공으로 멀티스레드 환경에서 안전하지만 성능 저하
	* 모든 메서드에 동기화가 적용됨.
	* Null 키와 값을 허용하지 않음.
	* Java 1.0 부터 도입됨.
	* **레거시 클래스**, 현재는 잘 사용되지 않음.


## 코드로 보는 차이점(JAVA)

**ConcurrentHashMap**

```java
import java.util.concurrent.ConcurrentHashMap;

public class ConcurrentHashMapExample {
    public static void main(String[] args) {
        ConcurrentHashMap<String, String> map = new ConcurrentHashMap<>();
        map.put("key1", "value1");
        map.put("key2", "value2");

        // Null 키나 값을 허용하지 않음
        // map.put(null, "value3"); // Throws NullPointerException
        // map.put("key3", null);   // Throws NullPointerException

        System.out.println("key1: " + map.get("key1"));

        // 원자적 연산
        map.putIfAbsent("key3", "value3");
        map.replace("key2", "value2", "newValue2");

        map.forEach((key, value) -> System.out.println(key + ": " + value));
    }
}
```

**HashMap**

```java
import java.util.HashMap;

public class HashMapExample {
    public static void main(String[] args) {
        HashMap<String, String> map = new HashMap<>();
        map.put("key1", "value1");
        map.put("key2", "value2");
        map.put(null, "value3"); // Null key
        map.put("key3", null);   // Null value

        System.out.println("key1: " + map.get("key1"));
        System.out.println("null key: " + map.get(null));   // Prints value3

        map.forEach((key, value) -> System.out.println(key + ": " + value));
    }
}
```

**Hashtable**

```java
import java.util.Hashtable;

public class HashtableExample {
    public static void main(String[] args) {
        Hashtable<String, String> map = new Hashtable<>();
        map.put("key1", "value1");
        map.put("key2", "value2");

        // Null 키나 값을 허용하지 않음
        // map.put(null, "value3"); // Throws NullPointerException
        // map.put("key3", null);   // Throws NullPointerException

        System.out.println("key1: " + map.get("key1"));

        map.forEach((key, value) -> System.out.println(key + ": " + value));
    }
}
```

### 요약

- **ConcurrentHashMap**은 멀티스레드 환경에서 높은 성능을 제공하며, 동시성 제어를 위해 버킷 단위로 락을 사용함. Null 키와 값을 허용하지 않음.
  
- **HashMap**은 단일 스레드 환경에서 사용되며, 동기화가 필요 없는 경우에 적합함. Null 키와 값을 허용함.
  
- **Hashtable**은 모든 메서드가 동기화되어 있으며, 멀티스레드 환경에서 안전하지만 성능이 저하됨. Null 키와 값을 허용하지 않음.
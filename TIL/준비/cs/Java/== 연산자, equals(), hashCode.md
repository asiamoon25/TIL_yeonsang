
## == 연산자

* 객체의 주소값을 비교, 같은 값이라도 주소값이 다르면 false 가 나옴.
* == 은 int 와 같은 prime type 을 비교할 때 사용됨.


---

# equals(), hashCode란?

Object 클래스에 정의되어 있음. 그렇기 때문에 Java 의 모든 객체는 Object 클래스에 정의된 equals 와 hashCode 함수를 상속 받고 있음.

## equals()

```java
public boolean equals(Object object) {
	if(this == anObject) {
		return true;
	}
	return (anObject instanceof String aString)
		&& (!COMPACT_STRINGS || this.coder == aString.coder)
		&& StringLatin1.equals(value, aString.value);
}
```

* 기본적으로 2개의 객체가 동일한지 검사하기 위해 사용됨.
* equals 가 구현된 방법은 2개의 객체가 참조하는 것이 동일한지를 확인하는 것이며, 이는 동일성을 비교하는 것임.
* 동일한 메모리 주소일 경우에만 동일한 객체가 됨.
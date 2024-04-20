
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
}
```

* 기본적으로 2개의 객체가 동일한지 검사하기 위해 사용됨.
* equals 가 구현된 방법은 2개의 객체가 참조하는 것이 동일한지를 확인하는 것이며, 이는 동일성을 비교하는 것임.
* 동일한 메모리 주소일 경우에만 동일한 객체가 됨.

하지만 Object 에서의 equals 는 주소를 비교하기 때문에 equals 로 내용을 비교하기 위해서는 equals()  를 오버라이딩 할 필요가 있다.

```java
Obj aa = new Obj(1);
Obj bb = new Obj(1);

System.out.println(aa == bb); // false 주소 비교 인데 다르기 때문에
System.out.println(aa.equals(bb)); // false equals Override 안하고 Object 꺼 사용해서 false 뜸.
```
```java
static class Obj {
	int a;
	public Obj(int a) {
		this.a = a;
	}
	@Override
	public boolean equals(Object o) {
		if(this == o) return true;
		if(o == null || getClass() != o.getClass()) return false;
		Obj tha = (Obj) o;
		return a == that.a;
	}
	@Override
	public int hashCode() {
		return Objects.has(a);
	}
}
```


## hashCode

* Runtime 중에 객체의 유일한 Integer 값을 반환함.
* Object 클래스에서는 heap 에 저장된 객체의 메모리 주소를 반환하도록 되어 있음.(항상은 아님)
```java
public native int hashCode();
```




---
그리고 equals() 재정의 할 때 hashCode 도 재정의 해야함.

```java
	@Override
	public boolean equals(Object o) {
		if(this == o) return true;
		if(o == null || getClass() != o.getClass()) return false;
		Obj tha = (Obj) o;
		return a == that.a;
	}
	@Override
	public int hashCode() {
		return Objects.has(a);
	}
```

만약 equals()와 hashcode() 중 하나만 재정의 하면 어떻게 될까?

**equals()만 재정의하지 않으면** hashcode()가 만든 해시값을 이용해 객체가 저장된 버킷을 찾을 수는 있지만 해당 객체가 자신과 같은 객체인지 값을 비교할 수 없기 때문에 **null을 리턴하게 된다.** 따라서 원하는 객체를 찾을 수 없음.

반대로 **hashcode()만 재정의 하지 않으면 위 예제를 해보면 알겠지만 같은 값 객체라도 hashcode값이 달라진다.** 따라서 HashTable 같은 자료구조에서 그 객체를 put한 상태에서 해당 객체가 저장된 버킷을 찾을 수 없다. (key값을 hashcode로 잡기 때문이다. `버킷`은 해쉬테이블에서 데이터가 저장된 곳이다.)

이러한 이유로 객체의 **정확한 동등, 동일 비교를 위해서는** (특히 Hash 관련 컬렉션 프레임워크를 사용할때!)

**Object의 equals() 메소드, hashCode()메소드 둘다 같이 재정의해야 한다.**



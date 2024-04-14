#Java #keyword

## Static 이란

![[Pasted image 20240414113907.png]]

### static?
* 사전적 정의로는 정적인 의 뜻을 가지고 있음.
	* 사전적인 의미로만 봐도 불변한다는 걸 알 수 있음.. 막 건들면 에러날거 같은...
* JAVA 에서는 최초 클래스를 로드할때 메모리에 할당해 종료될 때 해제 되는 것을 의미.


### 메모리 할당?
[JVM](obsidian://open?vault=TIL_yeonsang&file=TIL%2F%EC%A4%80%EB%B9%84%2Fcs%2FJava%2FJVM)
위 글의 Runtime Data 영역을 보면 method area, heap area가 보이는데 method area 의 설명을 보면

클래스 정보를 처음 메모리에 올릴 때 초기화 되는 대상을 저장하기 위한 영역
	* 올라가는 정보
		1. Field Information
			* 멤버 변수에 대한 정보(이름,타입,접근 지정자 등)
		2. Method Information
			* 메서드에 대한 정보(이름, 리턴타입, 파라미터, 접근 지정자 등)
		3. Type Information

이렇게 설명이 되있는데 이때 static 변수가 method area 에 저장되고, GC 의 관리를 받지 않고 프로그램 종료 시 까지 유지된다.
> GC 의 대상은 Heap 영역이다.


### static keyword 특징
1. 클래스 레벨 공유
	static 변수는 클래스의 모든 인스턴스에 의해 공유됨. 이 변수들은 클래스가 메모리에 로드될 때 생성되고, 프로그램이 종료될 때까지 유지됨.
2. 메모리 효율
	같은 클래스의 모든 객체들이 하나의 `static` 변수를 공유하기 때문에 메모리 사용이 줄어듬.
3. 인스턴스 없이 접근 가능
	static 메서드나 변수는 객체의 인스턴스를 생성하지 않고도 호출할 수 있음. 클래스 이름을 통해 직접 접근 가능.
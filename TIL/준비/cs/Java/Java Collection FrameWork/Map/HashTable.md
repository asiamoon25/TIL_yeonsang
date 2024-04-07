#Map #HashTable #JavaCollectionFramework 

# HashTable

## 란?
* Key, Value 로 데이터를 저장하는 자료구조
* 내부적으로 배열(버킷) 을 사용하여 데이터를 저장함.
	실제 값이 저장되는 장소를 버킷 또는 슬롯이라고 함.



## 특징

* 동기화
	HashTable 의 메소드는 Thread-safe 임. 여러 쓰레드가 동시에 HashTable 을 수정하더라도 데이터의 일관성이 유지됨. 반면에 HashMap 은 Thread-Safe 하지 않음.
* null 허용 안함.
	HashTable 은 key 나 value 값으로 null 을 허용하지 않음. key 또는 Value 값으로 `null` 을 사용하려고 하면 `NullPonterException` 이 발생함.
* 성능
	HashTable 의 동기화 특성 때문에 HashMap 에 비해 성능이 떨어질 수는 있음.
	단일 쓰레드 애플리케이션 또는 멀티쓰레드 환경에서 동기화가 필요하지 않는 경우, HashMap 이 더 나은 성능을 가짐.
* 유물임
	자바 초기 버전부터 제공되던 녀석이기 때문에 Map 인터페이스와 함께 새로운 컬렉션 프레임워크가 도입되면서, 
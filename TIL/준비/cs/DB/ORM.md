#orm

## 이란?

**Object-Relational Mapping**

* 객체와 관계형 데이터베이스의 데이터를 자동으로 매핑해주는 것.
	* 객체 모델과 관계형 모델 간에 불일치가 존재하기 때문에 ORM 을 통해 객체 간의 관계를 바탕으로 SQL 을 자동으로 생성하여 불일치를 해결해줌.
* DB Data <- Mapping -> Object field
	* 객체를 통해 간접적으로 데이터베이스 데이터를 다룸.
* Persistant API 라고도 불림
	* JPA,Hiberante


## ORM 작동 원리

1. 데이터베이스 테이블과 객체의 매핑
	* ORM 은 데이터베이스의 테이블을 클래스로 매핑함.
		* 테이블의 각 행(row) 는 클래스의 인스턴스로, 테이블의 열(column)은 인스턴스의 속성(attribute) 로 대응도미.\




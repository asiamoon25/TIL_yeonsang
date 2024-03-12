---
sticker: lucide//align-horizontal-justify-center
---
### GORM
* Grails 특화 : GORM 은 Grails 프레임워크의 일부, Groovy 언어의 동적 기능을 활용하여 데이터베이스 작업을 단순화함. Grails 를 위해서만 설계되었음.
* 동적 기능 : GORM 은 groovy 의 동적 프로그래밍 기능을 사용하여, 런타임에 CRUD 작업을 위한 메서드를 자동으로 생성함. -> 직관적이고 간결한 코드로 DB 작업을 할 수 있게 함.
* 다양한 백엔드 지원 : GORMdms Hibernate를 기반으로 하지만, SQL, NoSQL, REST API 등 다양한 데이터 스토어를 지원함.


###

메타클래스를 사용하면, 파이썬의 class 문을 가로채서, 클래스가 정의될 때마다 특별한 동작을 제공할 수 있다




### JPA (Java Persistence API)
* 자바 표준 : Java EE 의 공식 ORM 기술, 다양한 Java 애플리케이션에서 사용됨.
	JPA는 ORM 표준 인터페이스를 제공하며, Hibernate, EclipseLink, OpenJPA 등 다양한 구현체를 사용할 수 있음.
* 포터빌리티 : JPA 는 특정 구현체에 종속되지 않는 표준화된 API 를 제공함. 어플리케이션을 다른 JPA 구현으로 쉽게 이전할 수 있게 함.
* 정적 타입 : JPA 는 주로 Java 언어의 정적 타입 특성을 활용함. 엔티티 클래스를 정의하여 DB 테이블과 매핑하며, JPQL을 사용하여 쿼리를 작성함.


### 차이점
* 프로그래밍 언어와 프레임워크 : GORM 은 grails 와 Groovy  에 특화 되있으며, 동적 프로그래밍 기능을 적극 활용함. JPA 는 Java 표준이며, 다양한 Java 기반 애플리케이션에서 사용됨.
* 접근 방식 : GORM 은 런타임에 동적으로 메서드를 생성하여 개발자의 작업을 간소화하는 반면에 JPA 는 엔티티 매핑과 JPQL 을 통해 좀 더 전통적인 ORM 접근 방식을 취한다.
* 다양성과 확장성 : JPA는 그 자체로는 특정 구현체에 대한 표준 인터페이스를 제공하는 반면에 GORM 은 Grails 내에서 더 풍부하고 다양한 데이터 스토어를 직관적으로 다룰 수 있는 특화된 기능을 제공함.



왜 GORM 은 영속성 구현으로 JPA가 아닌 Hibernate를 사용하는 이유


Grails 는 ORM 도구로 GORM 을 사용하고 GORM 은 기본 영속성 구현으로 Hibernate 를 사용함.
Hibernate 가 풍부한 기능 세트, 강력한 커뮤니티 지원 및 JAVA 생태계에서 입증된 실적을 갖춘 널리 사용되는 ORM 프레임 워크이기 때문에...

Hibernate 는 강력하고 유연한 매핑 옵션을 제공하므로 GORM 의 단순성, 유연성 및 생산성 목표에 매우 적합함. JPA 는 Java의 ORM 에 대한 표준 사양이지만, Hibernate를 기본 영속성  구현으로 사용하기로 한 GORM 은 Grails 애플리케이션 내에서 JPA 사용을 배제하지 않음.

Grails 는 대체 영속성 옵션으로 JPA 를 지원하기 때문에 적합한 ORM 솔루션을 선택할 수 있음.


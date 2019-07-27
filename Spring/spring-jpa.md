---
   title: "[Spring]JPA란"             #글 제목
   date: 2019-03-20 15:00:00                             #작성일
   tags: ["Spring","framework","JPA","SpringDataJPA"]
   categories: Spring                                     #태그
---
# JPA란
JPA는 여러 ORM 전문가가 참여한 EJB 3.0 스펙 작업에서 기존 EJB ORM이던 Entity Bean을 JPA라고 바꾸고 JavaSE, JavaEE를 위한 영속성(persistence) 관리와 ORM을 위한 표준 기술이다. JPA는 ORM 표준 기술로 Hibernate, OpenJPA, EclipseLink, TopLink Essentials과 같은 구현체가 있고 이에 표준 인터페이스가 바로 JPA이다.

## ORM 이란
ORM(Object Relational Mapping)이란, Object(객체)와 Relation(관계형 데이터베이스)  간의 불일치 문제를 해결하기 위한 도구다.

흔히 알고 있는 ibatis나 mybatis는 ORM이 아니다. SQL 구문을 Mapping 하여 실행하는 sql mapper이다.

## 장단점
### 장점

객체지향적으로 데이터를 관리할 수 있기 때문에 비즈니스 로직에 집중 할 수 있으며, 객체지향 개발이 가능하다.
테이블 생성, 변경, 관리가 쉽다. (JPA를 잘 이해하고 있는 경우)
로직을 쿼리에 집중하기 보다는 객체자체에 집중 할 수 있다.
빠른 개발이 가능하다.
### 단점

어렵다. 장점을 더 극대화 하기 위해서 알아야 할게 많다.
잘 이해하고 사용하지 않으면 데이터 손실이 있을 수 있다. (persistence context)
성능상 문제가 있을 수 있다.(이 문제 또한 잘 이해해야 해결이 가능하다.)
## 어노테이션 정리
### @Entity
JPA에서 Entity라는 것은 데이터베이스에 저장하기 위해서 유저가 정의한 클래스다. 일반적으로 RDBMS에서 Table의 정의 비슷한 것이다. Table의 이름이나 컬럼들에 대한 정보를 가진다.

### @Id
일반적으로 키(primary key)를 가지는 변수에 선언한다. @GeneratedValue 어노테이션은 해당 Id 값을 어떻게 자동으로 생성할지 전략을 선택할 수 있다. 

### @Table
@Table을 이용하면 별도의 이름을 가진 데이터베이스 테이블과 매핑할 수 있다. 기본적으로 @Entity로 선언된 클래스의 이름은 실제 데이터베이스의 테이블 명과 일치하는 것을 매핑한다. 따라서 @Entity의 클래스명과 데이터베이스의 테이블명이 다르면 @Table(name="XXX") 같은 형식으로 작성하면 이름을 다르게 해서 매핑이 가능하다.

### @Column
@Column에서 지정한 멤버 변수와 데이터베이스의 컬럼명을 다르게 주고 싶다면 @Column(name="XXX") 같은 형식으로 작성해주면 된다. 그렇지 않으면 기본적으로 멤버 변수명과 일치하는 데이터베이스의 컬럼을 매핑 한다.

---
그외의 어노테이션들이나 사용법들은 추후에 더 포스팅 하도록 하겠습니당 
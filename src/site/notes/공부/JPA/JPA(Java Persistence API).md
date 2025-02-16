---
dg-publish: true
---
EJB 3.0에서 Hibernate를 기반으로 만든 자바 [[공부/JPA/ORM(Object Relational Mapping)\|ORM(Object Relational Mapping)]] 기술 표준

SQL 작성 없이 객체를 데이터베이스에 직접 저장할 수 있게 도와주며, 애플리케이션과 JDBC 사이에서 동작한다

자바 애플리케이션에서 RDB를 사용하는 방식을 정의한 인터페이스 모음이다
즉, 인터페이스를 구현하여 사용해야 한다

#### 구현체의 종류

Hibernate
EclipseLink
DataNucleus

#### 장점
- ==높은 생산성==
  JPA에 객체를 전달만 하면 되므로 SQL을 작성하고 JDBC API를 사용하는 반복적인 일을 하지 않아도 된다
  DDL도 JPA가 자동으로 생성해주기 때문에 DB 설계 중심을 객체 설계 중심으로 변경할 수 있다

- ==유지보수 용이==
  SQL을 직접 다루면 필드를 하나 추가 / 삭제할 때 관련 SQL과 JDBC 코드를 모두 수정해야 하지만, JPA를 사용하면 이를 대신 처리해주어 유지보수가 줄어든다

#### 단점
- ==속도 저하 가능성==
  프로젝트의 규모가 크고 복잡하여 설계가 잘못된 경우, 속도 저하 및 일관성을 무너뜨릴 수 있다
  복잡하고 무거운 쿼리는 속도를 줄이기 위해 별도의 튜닝이 필요하기 때문에 결국 SQL문을 써야할 수 있다
### 동작 과정
*JPA는 애플리케이션과 JDBC API 사이*에서 동작
개발자가 JPA를 사용하면 JPA 내부에서는 JDBC API를 사용해 SQL을 생성하여 DB와 통신한다

##### JPA CRUD
- persist = insert
- find = select
- remove = delete
- JPA는 update를 지원하지 않지만, 데이터를 조회해서 값을 변경한 후 커밋하면 DB 서버에서 UPDATE로 바꿔서 실행한다
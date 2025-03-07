---
{"dg-publish":true,"permalink":"/공부/SW/DAO(Data Access Object)/","dgPassFrontmatter":true}
---


DB 데이터에 접근하기 위한 객체

Spring에서는 *Repository 인터페이스*를 통해 DAO 기능을 구현하는 경우가 많다

==데이터에 접근하기 위한 로직==과 ==비즈니스 로직==을 분리하기 위해 사용하며,
직접 DB에 접근하여 data를 삽입, 삭제, 조회를 하거나 쿼리 수행, 연결 관리, 트랜잭션 관리 등 조작할 수 있는 기능을 수행한다

일반적으로 DAO는 인터페이스로 정의되며, 실제 데이터 액세스 로직은 해당 인터페이스를 구현한 클래스에서 구현된다

##### DAO를 인터페이스로 두는 이유
1) 의존성 역전 원칙(DIP) 적용
   고수준 모듈이 저수준 모듈에 의존하지 ㅇ낳고
##### Repository vs DAO

- 추상화 수준:
    - DAO: 데이터 저장소에 대한 낮은 수준의 접근을 추상화
    - Repository: 객체 컬렉션에 대한 높은 수준의 추상화를 제공
- 범위:
    - DAO: 주로 단일 테이블이나 저장 프로시저와 연관
    - Repository: 하나 이상의 DAO를 사용하여 집계된 도메인 객체를 다룸
- 비즈니스 로직:
    - DAO: 일반적으로 순수한 CRUD 작업만 수행
    - Repository: 도메인 객체와 관련된 비즈니스 로직을 포함할 수 있음
- 설계 철학:
    - DAO: 데이터 영속성에 중점
    - Repository: 도메인 모델에 중점
- 사용 패턴:
    - DAO: 전통적인 3-tier 아키텍처(Java EE 패턴)에서 주로 사용
    - Repository: DDD(Domain-Driven Design)와 같은 현대적인 아키텍처에서 선호됨
- 테스트 용이성:
    - Repository: 일반적으로 인터페이스로 정의되어 있어 mock 객체를 사용한 테스트가 더 쉬움

```java

```
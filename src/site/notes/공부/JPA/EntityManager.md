---
{"dg-publish":true,"permalink":"//jpa/entity-manager/","dgPassFrontmatter":true}
---


[[공부/JPA/Entity\|Entity]] 객체를 관리하는 역할
Entity 객체를 [[공부/JPA/Persistence Context\|Persistence Context]]에 넣어두고, 객체의 생사를 관리함

#### 주입
EntityManager를 빈으로 주입하려면 **@PersistenceContext** 를 사용한다
-> 주입받은 EntityManager는 Proxy로 감싸지기 때문에 EntityManager를 호출할 때마다 proxy를 통해 EntityManager를 생성하여 Thread-Safe를 보장한다
동시성 문제가 발생하지 않음!

#### 동작
JPA는 기본적으로 한 요청 당 하나의 EntityManager를 사용한다
각 EntityManager들은 정해진 영속성 컨텍스트를 참조하게 된다
EntityManager로 데이터를 다루려면 가장 먼저 Entity가 ==영속화==되어있어야 한다

==일반적으로는 EntityManager 한 개당 하나의 영속성 컨텍스트를 갖지만, 스프링에서는 공통된 영속성 컨텍스트 하나를 여러 EntityManager가 참조한다.==

##### persist(entity)
영속성 컨텍스트를 통해 entity를 영속화하는 메소드
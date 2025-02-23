---
{"dg-publish":true,"permalink":"//jpa/annotation/generated-value/","dgPassFrontmatter":true}
---


---
{"dg-publish":true,"permalink":"/공부/JPA/Annotation/@GeneratedValue/","dgPassFrontmatter":true}
---

기본키 자동 생성 어노테이션

#### @GeneratedValue(strategy = GenerationType.IDENTITY)
기본키 생성을 데이터베이스에게 위임하는 방식
주로 MySQL, PostegreSQL, SQL Server, DB2에서 사용한다

id값을 따로 할당하지 않아도 데이터베이스가 자동으로 **AUTO_INCREMENT**를 하여 기본키를 생성해준다.

AUTO_INCREMENT를 사용할 때 애플리케이션에서는 그 값이 얼마인지 알고 보낼 수 없기 때문에 DB에 insert문을 날려야 id 값을 알 수 있다

즉, 원래 객체를 save()로 저장할 때는 id값을 알고 있기 때문에 트랜잭션이 끝나는 commit 시점에 flush가 이뤄지지만, 해당 설정을 하면 DB에서 id 값을 받아와야 하기 때문에 예외적으로 **save() 메서드를 호출하는 시점에 flush가 나간다!**(insert 쿼리를 날린다)

이렇게 반환 받은 식별자 값을 가지고 영속성 컨텍스트 1차 캐시에 엔티티를 등록하여 관리한다

JPA는 보통의 경우 트랜잭션이 commit 되는 시점에 쓰기 지연 저장소에 모아놓은 SQL을 한 번에 DB로 전송하여 애플리케이션과 DB 사이에 오가는 횟수를 줄여 성능을 높이는데, 이 전략은 insert를 하기 전엔 pk를 알 수 없으므로 save()를 하는 시점에 flush를 하는 것이다
#### @GeneratedValue(strategy = GenerationType.SEQUNCE)
DB의 sequence 객체를이용해 Id값을 증가시키는 전략
이 전략은 sequence를 사용하는 Oracle, DB2, H2에서 가능하며, [[공부/JPA/Annotation/@SequenceGenerator\|@SequenceGenerator]]와 함께 사용할 수 있다

만약 sequence 객체를 사용하지 않는 DB 벤더를 이용할 경우 sequence를 관리할 테이브를 생성한다(jpa ddl auto 일 때)
##### 그 외 
@GeneratedValue(strategy = GenerationType.TABLE)
@GeneratedValue(strategy = GenerationType.AUTO)
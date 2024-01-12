---
{"dg-publish":true,"permalink":"/공부/JPA/Annotation/Entity 관련 Annotation/","dgPassFrontmatter":true}
---

**@Id**
해당 컬럼이 식별키(PK)라는 것을 의미함
모든 엔티티에 반드시 @Id를 지정해야 함

**@Column**
인스턴스 변수가 컬럼이 되기 때문에, 컬럼명을 별도로 지정하거나 컬럼의 사이즈/제약조건들을 추가하기 위해 사용

**@Table**
클래스가 테이블이 되기 때문에 클래스 선언부에 작성
테이블명 결정
지정을 하지 않을 경우 클래스명으로 테이블이 생성된다

**@Entity**
해당 클래스의 인스턴스들이 엔티티임을 명시함

**[[공부/JPA/Annotation/@EntityListeners\|@EntityListeners]]**
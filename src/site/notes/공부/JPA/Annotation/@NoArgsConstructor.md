---
{"dg-publish":true,"permalink":"/공부/JPA/Annotation/@NoArgsConstructor/","dgPassFrontmatter":true}
---

아무 매개변수가 없는 생성자를 생성하는 어노테이션

````java
@NoArgsConstructor(access = AccessLevel.PROTECTED)
````

이렇게 자주 쓰이는데 아무 매개 변수가 없는 생성자를 생성하되 **다른 패키지에 소속된 클래스 접근을 막는** 방식이다

#### 접근 권한이 private이 아닌 이유
Entity의 Proxy 조회 때문
엔티티의 연관 관계에서 [[공부/JPA/지연 로딩(fetch = FetchType.LAZY)\|지연 로딩(fetch = FetchType.LAZY)]]의 경우에는 실제 엔티티가 아닌 **프록시 객체를 통해서 조회**를 한다

프록시 객체를 사용하기 위해서 JPA 구현체는 실제 엔티티의 기본 생성자를 통해 프록시 객체를 생성하는데, 이때 접==근 권한이 private 이면 프록시 객체를 생성할 수가 없다!==

물론 즉시로딩으로 구현하면 접근 권한과 상관 없이 프록시 객체가 아닌 실제 엔티티를 생성하므로 문제가 되지 않는다
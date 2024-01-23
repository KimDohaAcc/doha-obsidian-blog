---
{"dg-publish":true,"permalink":"/공부/JPA/지연 로딩(fetch = FetchType.LAZY)/","dgPassFrontmatter":true}
---

@ManyToOne(fetch = FetchType.*LAZY*)와 같이 FetchType을 설정하는 것
[[공부/JPA/Entity\|Entity]]가 실제 사용될 때까지 데이터베이스 조회를 지연하는 방법을 **지연 로딩**이라고 한다

지연 로딩을 사용하려면 실제 엔티티 객체 대신 데이터베이스 조회를 지연할 수 있는 **가짜 객체**가 필요한데 이를 ==프록시 객체==라 한다.
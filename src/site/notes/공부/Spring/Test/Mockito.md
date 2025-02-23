---
{"dg-publish":true,"permalink":"//spring/test/mockito/","dgPassFrontmatter":true}
---


---
{"dg-publish":true,"permalink":"/공부/Spring/Test/Mockito/","dgPassFrontmatter":true}
---

[[공부/Spring/Test/Mock\|Mock]]객체를 쉽게 생성, 관리, 검증할 수 있는 툴을 제공하는 [[공부/SW/Framework\|Framework]]

에플리케이션에서 데이터베이스, 외부 API 등을 테스트 할 때, 해당 제품들이 어떻게 작동하는지 항상 사용하며 테스트를 작성한다면 매우 불편할 것이다
이럴 때 Mock 객체를 만들어서 사용하면 해당 객체를 구현하지 않고 테스트를 작성할 수 있다

Springboot 2.2 이상 버전의 프로젝트를 생성 시 sping-boot-start-test에서 자동으로 Mokito를 추가해준다

#### Mock 객체 만들기
---
{"dg-publish":true,"permalink":"/공부/Spring/스프링 기초/Spring Container/","dgPassFrontmatter":true}
---

스프링 컨테이너 또는 [[공부/Spring/스프링 기초/ApplicationContext\|ApplicationContext]]라고 불리는 ==스프링 런타임 엔진==이다.
설정 정보를 참고해서 애플리케이션을 구성하는 객체를 생성하고 관리한다.
독립적으로 동작할 수도 있지만, 보통 웹 모듈에서 동작하는 서비스나 서블릿으로 등록해서 사용한다.

#### Container
스프링에서 핵심적인 역할을 하는 객체를 [[공부/Spring/스프링 기초/Bean\|Bean]] (자바의 class) 이라고 하며, Container는 Bean의 인스턴스화, 조립, 관리, 사용, 소멸에 대한 처리를 담당한다

#### BeanFactory
프레임워크 설정과 기본 기능을 제공하는 컨테이너 모든 유형의 객체를 관리할 수 있는 매커니즘 제공

[[공부/Spring/스프링 기초/ApplicationContext\|ApplicationContext]]를 하위 인터페이스로 갖는다
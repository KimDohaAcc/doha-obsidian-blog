---
{"dg-publish":true,"permalink":"/공부/Architecture/SOA(Service Oriented Architecture)/","dgPassFrontmatter":true}
---


1990년에 정의되어 2008년대에 유행했던 아키텍처 스타일.
2010년대에 들어서는 **Open API의 등장과 함께 경량화**되어 Open API 기반의 플랫폼에 많은 영향을 주고 있다

현대의 많은 분산 아키텍처가 거의 SOA 사상에 기인한다고 보면 된다

## SOA 기본 개념
기존의 시스템이 각각의 **독립된 업무 시스템**으로 개발되어왔던 반면,
SOA는 기능을 비즈니스적인 **의미가 있는 기능 단위**로 묶고 서비스라는 단위로 재조합한 후, 이 서비스들을 조합해 기능을 구현한다

이를 통해 새로운 업무를 구현할 때 시스템을 신규 개발하는 것이 아니라, ==기존에 제공된 서비스를 조합해 하나의 업무를 구현할 수 있다==. **소프트웨어의 재사용성**과 **레고웨어**의 연장선에 있는 것이다.

## SOA에서의 서비스
서비스는 '느슨하게 연결되고 상호 조합이 가능한 소프트웨어'이다

기존의 소프트웨어 개발은 애플리케이션을 **데이터 계층, 비즈니스 계층, 뷰 계층**과 같이 수평적으로 분리하였다.

그러나 SOA에서는 각각의 서비스 안에서 데이터, 비즈니스, 뷰에 대한 모듈을 가지고 있어서 각 ==서비스 간의 의존성이 최소화==된다.
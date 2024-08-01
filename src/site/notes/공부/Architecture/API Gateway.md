---
dg-publish: true
---
프록시 서버처럼 API 앞에서 모든 API에 대한 엔드포인트를 통합하고 추가적인 기능을 제공하는 미들웨어

SOA의 ESB(Enterprise Service Bus)의 경량화 버전이다

마이크로 서비스 아키텍처는 각 서비스가 다른 서버에 분리, 배포되기 때문에 API의 엔드포인트가 매우 많은데, P2P(Point to Point) 방식을 취하게 되면 토폴로지가 복잡해진다.

이러한 토폴로지의 문제점을 해결하기 위해 중앙에 **서비스 버스**와 같은 역할을 하는 채널인 API Gateway를 배치시켜서 ==P2P에서 Hub & Spoke 방식==으로 변환시켜서 서비스 간 호출을 단순화 할 수 있다

#### 오케스트레이션
여러 개의 서비스를 묶어서 하나의 새로운 서비스를 만드는 개념

#### 공통 기능 처리(Cross Cutting Function Handling)
API에 대한 인증(Authentication)이나 로깅과 같은 공통 기능에 대해서 API Gateway에서 처리할 수 있다.
---
{"dg-publish":true,"permalink":"///circuit-breaker/","dgPassFrontmatter":true}
---


장애 발생 지점을 감지하고 실패하는 요청을 계속적으로 보내지 않도록 **방지**하는 패턴

![Pasted image 20241029155440.jpg](/img/user/%EC%B2%A8%EB%B6%80%ED%8C%8C%EC%9D%BC/Pasted%20image%2020241029155440.jpg)

[[공부/Architecture/마이크로 서비스 아키텍처(MSA)\|마이크로 서비스 아키텍처(MSA)]] 에서 많이 사용되는 장애 대응 패턴이다

정상 상태에서는 평소처럼 API를 호출하면서, 오류 발생 횟수를 모니터링 한다.
일정 시간 내에 오류가 임계값을 초과하면 Circuit Breaker가 열리며, ==API 호출을 차단하고 즉시 에러를 반환하거나 대체 응답을 보낸다==.
이를 통해 불필요한 API 호출을 막아 *시스템을 보호*하는 패턴이다

Circuit Breaker를 구현한 대표적인 라이브러리로는 **Resilience4J**가 있다
---
{"dg-publish":true,"permalink":"///forward-proxy/","dgPassFrontmatter":true}
---


---
dg-publish: true
---
클라이언트의 요청을 직접 서버로 전달하지 않고, ==프록시 서버를 거쳐서 전달하는 것==

클라이언트 바로 뒤에 놓여있는 프록시 서버를 사용한다
[[공부/웹/리버스 프록시(Reverse Proxy)\|리버스 프록시(Reverse Proxy)]]와 반대 개념이다

이 경우 서버는 클라이언트의 IP가 아닌 프록시 서버의 IP로 요청을 받기 때문에, *클라이언트 정보에 대한 보안*이 중요한 경우 사용된다
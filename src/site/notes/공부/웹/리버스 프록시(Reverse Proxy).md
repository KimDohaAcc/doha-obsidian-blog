---
{"dg-publish":true,"permalink":"/공부/웹/리버스 프록시(Reverse Proxy)/","dgPassFrontmatter":true}
---

클라이언트의 요청을 바로 서버로 전달하지 않고, 중개자 역할을 하는 것

웹서버 앞에 놓여있는 프록시 서버를 가진다
[[공부/웹/포워드 프록시(Forward Proxy)\|포워드 프록시(Forward Proxy)]]와 반대 개념이다

이를 통해 요청을 처리할 적절한 서버로 보내줄 수 있다(로드밸런싱)
또 다른 역할로 URL을 재작성 하거나, 액세스 제어 기능을 할 수 있다

리버스 프록시를 사용할 경우 서버의 주소를 노출시키지 않을 수 있기에 ==서버 측 보안==에 유리하다

![Pasted image 20241031155124.png](/img/user/%EC%B2%A8%EB%B6%80%ED%8C%8C%EC%9D%BC/Pasted%20image%2020241031155124.png)
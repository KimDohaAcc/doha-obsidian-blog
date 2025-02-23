---
{"dg-publish":true,"permalink":"///web-server/","dgPassFrontmatter":true}
---


인터넷을 기반으로 클라이언트에게 웹 서비스를 제공하는 컴퓨터 혹은 프로세스

![Pasted image 20241031131607.png](/img/user/%EC%B2%A8%EB%B6%80%ED%8C%8C%EC%9D%BC/Pasted%20image%2020241031131607.png)

웹 서버가 제공할 수 있는 데이터는 정적 파일에 한정된다
그렇기 때문에 동적 페이지를 처리하기 위한 [[공부/웹/WAS(Web Application Server)\|WAS(Web Application Server)]]가 등장했다

## 웹 서버 예시

#### Apache Server

Nginx가 탄생하기 전 주로 사용되던 웹서버
클라이언트의 요청이 들어오면, 요청마다 쓰레드를 만들어서 처리했다
따라서 사용자가 많으면 ==메모리 및 CPU 낭비==가 심하다

#### Nginx

이러한 Apache Server의 문제점을 해결하기 위해 함께 사용되었다
그 당시 완전히 대체할 목적은 아니었으며, 문제점 보완 정도로 사용되었다

정적 파일에 대한 요청을 동시다발적으로 받으면 [[공부/웹/Nginx\|Nginx]]가 처리하였으며,
그 외 동적 파일 요청에 대해서만 Apache Server와 커넥션을 형성하였다
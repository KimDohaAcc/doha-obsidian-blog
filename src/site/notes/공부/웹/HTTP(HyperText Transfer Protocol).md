---
dg-publish: true
permalink: /공부/웹/HTTP/
dgPassFrontmatter: true
---

클라이언트와 서버 사이에 이루어지는 요청/응답(request/response) 프로토콜

이제는 HTML 텍스트 뿐만 아니라 이미지, 음성, 영상, 파일, JSON 등
*거의 모든 형태의 데이터 전송이 가능*하다
서버 간 데이터를 주고 받을 때도 대부분 HTTP를 사용한다

### HTTP 역사

HTTP/0.9 1991년: GET 메소드만 지원, HTTP 헤더 없음
HTTP/1.0 1996년: 메소드, 헤더 추가
**HTTP/1.1 1997년: 가장 많이 사용되는 버전** <- 대부분의 스펙이 다 들어있음
HTTP/2 2015년: 성능 개선
HTTP/3 진행 중: TCP 대신 UDP 사용, 성능 개선

### 기반 프로토콜

TCP: HTTP/1.1, HTTP/2
UDP: HTTP/3

### 특징

클라이언트 서버 구조
무상태(Stateless) 프로토콜, 비연결성
단순함, 확장 가능
HTTP 메시지
---
{"dg-publish":true,"permalink":"/공부/Spring/스프링 기초/RestTemplate/","dgPassFrontmatter":true}
---

Spring에서 지원하는 객체로 간편하게 Rest 방식 API를 호출할 수 있는 Spring 내장 클래스입니다.

Spring 3.0부터 지원되었고, json, xml 응답을 모두 받을 수 있습니다.

Rest API 서비스를 요청 후 응답 받을 수 있도록 설계되어있으며 HTTP 프로토콜의 메소드(ex. GET, POST, DELETE, PUT)들에 적합한 여러 메소드들을 제공합니다.

#### RestTemplate 동작 원리

1. 애플리케이션 내부에서 REST API에 요청하기 위해 RestTemplate의 메서드를 호출한다.

2. RestTemplate은 MessageConverter를 이용해 java object를 request body에 담을 message(JSON etc.)로 변환한다. 메시지 형태는 상황에 따라 다름

3. ClientHttpRequestFactory에서 ClientHttpRequest을 받아와 요청을 전달한다.

4. 실질적으로 ClientHttpRequest가 HTTP 통신으로 요청을 수행한다.

5. RestTemplate이 에러핸들링을 한다.

6. ClientHttpResponse에서 응답 데이터를 가져와 오류가 있으면 처리한다.

7. MessageConverter를 이용해 response body의 message를 java object로 변환한다.

8. 결과를 애플리케이션에 돌려준다.

※ RestTemplate은 통신 과정을 ClientHttpRequestFactory(ClientHttpRequest, ClientHttpResponse)에 위임합니다. ClientHttpRequestFactory의 실체는 HttpURLConnection, Apache HttpComponents, HttpClient와 같은 HTTP Client

**[출처]** [[Spring]스프링 RestTemplate](https://blog.naver.com/hj_kim97/222295259904)|**작성자** [로그](https://blog.naver.com/hj_kim97)
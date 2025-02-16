---
dg-publish: true
---
**비동기 이벤트 기반(Event-Driven) 아키텍처**의 웹 서버 소프트웨어

### 특징

###### 싱글 스레드
하나의 master process가 하나 또는 다수의 worker process를 관리한다
각 worker process는 single thread 방식으로 동작하며 여러 클라이언트의 요청을 동시에 처리한다

###### 이벤트 기반
Nginx에서 새로운 요청을 처리하는 것을 ==이벤트==라고 부른다
이벤트는 queue에 들어가 worker process에 전달 되며,
worker process는 이 이벤트들을 queue에서 꺼내 처리한다

이때 작업이 완료될 때까지 기다리지 않고 이벤트 큐에서 다음 이벤트를 처리하도록 하는 *비동기 이벤트 기반* 아키텍처로 구성되어 있다
작업이 완료될 때까지 기다리지 않고 계속 일하기 때문에, Apache [[공부/웹/웹 서버(Web Server)\|웹 서버(Web Server)]]보다 효율적으로 자원을 사용한다

###### 리버스 프록시
Nginx는 [[공부/웹/리버스 프록시(Reverse Proxy)\|리버스 프록시(Reverse Proxy)]]를 지원한다
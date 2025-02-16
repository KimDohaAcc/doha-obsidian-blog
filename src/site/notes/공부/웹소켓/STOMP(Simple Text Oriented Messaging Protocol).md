---
{"dg-publish":true,"permalink":"/공부/웹소켓/STOMP(Simple Text Oriented Messaging Protocol)/","dgPassFrontmatter":true}
---


메세징 전송을 효율적으로 하기 위한 프로토콜
WebSocket 위에서 동작하는 프로토콜로써 클라이언트와 서버가 전송할 메세지의 유형, 형식, 내용을 정의하는 매커니즘이다

또한 STOMP는 [[공부/웹/HTTP(HyperText Transfer Protocol)\|HTTP(HyperText Transfer Protocol)]]와 비슷하게 fram 기반 프로토콜 command, header, body로 이루어져 있어, 메세지의 헤더에 값을 줄 수 있고 헤더 값을 기반으로 통신 시 인증 처리를 구현하는 것도 가능하다

publisher / subscriber 라는 메세지 공급 주체와 소비 주체를 분리하는 구조로 되어 있어 메세지를 전송하고 받아서 처리하는 부분이 명확하다

Message Payload 에는 Text 또는 Binary 데이터를 포함할 수 있다
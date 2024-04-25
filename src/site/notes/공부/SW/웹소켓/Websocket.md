---
{"dg-publish":true,"permalink":"/공부/SW/웹소켓/Websocket/","dgPassFrontmatter":true}
---

웹소켓은 [[공부/SW/웹/HTTP\|HTTP]]와 구분되는 **통신 프로토콜**이다. HTTP와 웹소켓은 모두 OSI 참조 모델의 7계층에 위치해있고, TCP에 의존한다.

HTTP 통신은 요청(Request)와 응답(Response)가 존재하는 ==반이중통신(Half-Duplex Communication)== 구조를 가지고 있다. 

이와 다르게 웹소켓은 ==전이중통신(Full-Duplex Communication)==을 지원한다. 웹소켓으로 연결된 서버와 클라이언트는 각 주체가 요청과 응답없이 능동적으로 메세지를 보낼 수 있다.

따라서 웹소켓은 **전이중통신과 실시간 네트워킹**이 보장되어야 하는 환경에서 유용하게 사용될 수 있다.

#### 연결 수립
최초 요청 연결 시 클라이언트에서 HTTP를 통해 웹서버에 요청한다. 이를 [[공부/SW/네트워크/Handshaking\|Handshaking]]라고 한다.

핸드셰이크를 위해 클라이언트는 서버에 요청을 보내고 서버가 응답하여 핸드셰이크가 성공하면, 둘 간의 통신 프로토콜은 Websocket으로 전환된다

#### 전이중통신
연결이 수립되면 클라이언트와 서버 양측 간의 데이터 통신 단계가 시작되고, 보내는 메세지는 ==프레임== 단위로 이루어진다.

또한 연결 수립 이후 서버와 클라이언트는 언제든 상대방에세 ping 패킷을 보낼 수 있다. ping을 수신한 측은 가능한 빨리 pong 패킷을 상대방에게 전송해야 한다. 이런 방식으로 **서로의 연결이 살아있는지를 주기적으로 확인**할 수 있는데, 이를 HeartBeat라고 한다

#### 연결 종료
클라이언트 혹은 서버 중 연결 종료를 원하는 측이 Close  Frame을 상대쪽으로 전송하면 연결이 종료된다

#### 문제점
session 단위의 메시지만 전달이 가능하기 때문에 채팅방을 여러 개 생성할 수가 없다!
이를 해결하기 위해 [[공부/SW/웹소켓/STOMP(Simple Text Oriented Messaging Protocol)\|STOMP(Simple Text Oriented Messaging Protocol)]]를 이용해서 pub/sub 구조로 여러 개의 방을 만들어 STOMP의 Broker를 통해 메세지를 전달할 수 있다

하지만 STMOP는 기본적으로 서버 메모리를 Broker로 사용하기 때문에, ==서버가 2개 이상일 경우 채팅 전달에 있어서 클러스터링을 해줘야 하는 단점==이 존재하기에 이를 보완하려 [[공부/SW/메시지 큐/Kafka(event broker)\|Kafka(event broker)]]나 RabbitMQ 같은 메시지 큐 오픈 소스를 사용한다
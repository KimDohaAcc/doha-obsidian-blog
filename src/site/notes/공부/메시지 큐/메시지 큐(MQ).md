---
{"dg-publish":true,"permalink":"/공부/메시지 큐/메시지 큐(MQ)/","dgPassFrontmatter":true}
---


분산화된 환경에서 발신자와 수신자 간 메시지를 전송하고 수신하는 기술이며, [[공부/메시지 큐/MOM(message oriented middleware)\|MOM(message oriented middleware)]] 구현 방식 중 하나이다

#### 메시지 큐를 사용하는 이유

메시지 큐를 사용하면 발신자와 수신자가 서로를 직접 알 필요가 없으므로 ==느슨한 결합==을 만들어낼 수 있다.
발신자와 수신자가 서로에게 의존하지 않으므로 N:1:M의 형태로 **독립적 확장**이 가능하다

또한 수신자 서비스가 장애 상황이더라도 발행된 메시지는 모두 메시지 큐에 남아 있으므로 결국 발신자가 발신한 모든 메시지는 소비자 서비스에 전달된다는 **보장성**을 갖는다

#### 종류를 고를 때 고려할 것

RabbitMQ - 수신자가 수동적(등기 서비스)
Kafka - 수신자가 가져가야 함(택배 서비스)

#### Point to Point 와 Pub/Sub

메시지 큐는 크게 Point to Point 와 Pub/Sub 모델로 구분할 수 있다

Point To Point  : 한 대의 발신자가 한 대의 수신자에게 메시지를 보내는 방식

Pub/Sub : 발신자가 topic에 메세지를 전송하면 토픽을 구독하고 있는 수신자 모두 메시지를 수신하는 방식. ==전송 대상이 다수==


#### 대표적인 종류
[[공부/메시지 큐/Kafka(event broker)\|Kafka(event broker)]]
RabbitMQ(message broker)
ActiveMQ(meessage broker)
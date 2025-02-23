---
{"dg-publish":true,"permalink":"///udp-user-datagram-protocol/","dgPassFrontmatter":true}
---


---
dg-publish: true
---
사용자 데이터그램 프로토콜이라고 한다

기능이 거의 없다

[[공부/네트워크/TCP(Transmission Control Protocol)\|TCP(Transmission Control Protocol)]]와 다르게 [[공부/네트워크/TCP 3-way Handshake\|TCP 3-way Handshake]]도 없고, 데이터 전달 보증도 없고, 순서 보장도 없다

IP와 거의 같으며 여기에 [[공부/네트워크/PORT\|PORT]]와 체크섬 정도만 추가되는 것이다

#### 사용 이유

데이터 전달 및 순서가 보장되지 않지만, 단순하고 빠르다
TCP는 핸드셰이킹을 해서 속도가 보다 느리고 여러 데이터를 넣기 때문에 데이터의 양도 많다
그리고 추가 작업을 하고  싶을 때 손을 댈 수가 없다
UDP는 사용자 추가 작업 가능
---
{"dg-publish":true,"permalink":"//java/stream/flat-map/","dgPassFrontmatter":true}
---


Map + Flatten
**데이터에 함수를 적용한 후 중첩된 stream을 연결**하여 하나의 stream으로 리턴

모든 회원이 가지고 있는 주문 리스트 정보를 가져오는 리스트로, 회원마다 가지고 있는 주문을 flat 하게 펼치는 작업을 한다
````java
List<Order> collect = members.stream() // Stream<Member>
.map(Member::getOrders) // Stream<List<Order>
.flatMap(List::stream) // Stream<Order> 위의 orderList를 flat하게 펼쳐서 반환
.collect(Collectors.toList());
````
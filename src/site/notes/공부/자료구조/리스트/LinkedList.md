---
{"dg-publish":true,"permalink":"/공부/자료구조/리스트/LinkedList/","noteIcon":""}
---

LinkedList는 [[ArrayList\|ArrayList]]와는 달리 [[List\|List]] 인터페이스를 구현한 AbstrackList를 상속하지 않고, **AbstrackSequentialList**를 상속하고 있음

[[공부/자료구조/리스트/Node\|Node]] 로 구성되어 있다

#### 종류
[[공부/자료구조/리스트/단순 연결 리스트(Singly LinkedList)\|단순 연결 리스트(Singly LinkedList)]]
[[공부/자료구조/리스트/이중 연결 리스트(Doubly LinkedList)\|이중 연결 리스트(Doubly LinkedList)]]

ArrayList는 데이터들이 순서대로 있는 배열의 형식을 취하고 있다면,
LinkedList는 자료의 주소값으로 서로 연결되어 있는 구조이다

![Pasted image 20230913173026.png](/img/user/%EC%B2%A8%EB%B6%80%ED%8C%8C%EC%9D%BC/Pasted%20image%2020230913173026.png)

##### 장점
ArrayList는 사이즈가 고정되어 있기 때문에 자료 삽입 시 사이즈를 늘려주는 연산이 추가되어야 하고, 자료 삭제 시 빈 인덱스를 채우는 연산이 추가되어야 하는 반면
LinkedList는 주소만 연결시켜 주면 되므로 추가/삭제가 ArrayList보다 빠르고 용이하다.
따라서 삽입/삭제가 빈번한 프로세스의 경우 LinkedList를 사용하여 구현!

##### 단점
단순 LinkedList는 단방향성을 갖고 있기 때문에 인덱스를 이용하여 자료를 검색하는 방식은 적절하지 않다.
참조자를 위해 추가적인 메모리를 할당해야 하기 때문에 저장 공간의 낭비가 있다.
특정 자료를 탐색하는 시간이 많이 소요된다.

#### 성능
인덱싱 : Θ(n)
맨 앞에 삽입/삭제 : Θ(1)
중간에 삽입/삭제 : 탐색 + Θ(1)
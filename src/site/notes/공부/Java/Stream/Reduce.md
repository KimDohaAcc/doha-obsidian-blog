---
{"dg-publish":true,"permalink":"//java/stream/reduce/","dgPassFrontmatter":true}
---


주어진 함수를 반복 적용해 Stream 안의 데이터를 하나의 값으로 합치는 작업

인자 1개 
함수식
주어진 식으로 데이터를 합쳐 반환한다
````java
Integer sum = numbers.stream()
.reduce((x, y) -> x + y)
.get();
````

인자 2개 
초기값, 함수식
주어진 초기값과 함수식을 이용한다. 항상 반환 값이 존재한다
````java
Integer sum = numbers.stream()
.reduce(0, (x, y) -> x + y);
````

인자 3개
초기값, 타입 변경, 함수식
합치는 과정에서 타입이 바뀔 경우 사용한다
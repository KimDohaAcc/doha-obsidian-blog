---
{"dg-publish":true,"permalink":"//java/function-interface/","dgPassFrontmatter":true}
---


---
{"dg-publish":true,"permalink":"/공부/JAVA/Function Interface/","dgPassFrontmatter":true}
---

java.util.function 패키지에 있는 인터페이스로, T라는 타입의 인풋을 받아 R이란 타입을 반환하는 apply 메서드를 가진다

매개변수를 2개 받고 싶다면 [[공부/Java/BiFunction Interface\|BiFunction Interface]]를 사용한다
#### 구현
````java
Function<Integer, Integer> multiple = x -> x*2;

Integer result = multiple.apply(3);
````
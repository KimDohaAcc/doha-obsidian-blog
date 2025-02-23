---
{"dg-publish":true,"permalink":"/공부/Java/BiFunction Interface/","dgPassFrontmatter":true}
---


java.util.function 패키지에 존재하는 인터페이스로, 매개변수가 2개이고 반환 값이 있는 경우에 사용

````java
BiFunction<Integer, Integer, Integer> multiple = (x, y) -> x*y;
Integer result = multiple.apply(3, 5);
````
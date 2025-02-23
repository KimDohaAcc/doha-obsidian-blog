---
{"dg-publish":true,"permalink":"//java/stream/for-each/","dgPassFrontmatter":true}
---


제공된 action을 Stream의 각 데이터에 적용해주는 메소드

java의 iterable 인터페이스에서도 forEach가 존재하기 때문에 Set, List 등의 collection에서 바로 쓰는 것도 가능하다

stream의 중간 처리가 필요할 때는 stream에서 쓰면 된다

````java
numbers.stream().forEach(number -> System.out.println("number = " + number));
````
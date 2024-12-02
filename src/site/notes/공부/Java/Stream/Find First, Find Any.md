---
{"dg-publish":true,"permalink":"/공부/JAVA/Stream/Find First, Find Any/","dgPassFrontmatter":true}
---

#### findFirst
Stream 안의 첫번째 데이터를 반환
Stream이 비어있다면 비어있는 Optional을 반한

````java
Optional<Integer> findInteger = Stream.of(3, 2, -5, 6)
.filter(x -> x > 0)
.findFirst();
````

#### findAny
Stream 안의 아무 데이터나 리턴
Stream이 비어있다면 비어있는 Optional을 반한

````java
Optional<Integer> findInteger = Stream.of(3, 2, -5, 6)
.filter(x -> x > 0)
.findAny();
````
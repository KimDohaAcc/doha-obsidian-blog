---
{"dg-publish":true,"permalink":"//java/stream/max-min-count/","dgPassFrontmatter":true}
---


---
{"dg-publish":true,"permalink":"/공부/JAVA/Stream/Max, Min, Count/","dgPassFrontmatter":true}
---

#### max
Stream 안의 데이터 중 최댓값을 반환
Stream이 비어있다면 빈 Optional을 반환

````java
Optional<Integer> max = Stream.of(50, 30, 10)
.max(Integer::compareTo);
````

#### min
Stream 안의 데이터 중 최솟값을 반환
Stream이 비어있다면 빈 Optional을 반환

````java
Optional<Integer> min = Stream.of(50, 30, 10)
.min(Integer::compareTo);
````

#### count
Stream 안의 데이터 개수를 반환

````java
long count = Stream.of(50, 30, 10)
.count();
````
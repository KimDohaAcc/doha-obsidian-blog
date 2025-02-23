---
{"dg-publish":true,"permalink":"/공부/Java/Stream/Collector/collect/","dgPassFrontmatter":true}
---


자주 쓰일법한 유용한 collector를 모아놓은 util class
#### collect
주어진 collector를 이용해 Stream안의 데이터를 합친다

#### toList
Sream안의 데이터를 List 형태로 반환해주는 collector
````java
List<Integer> numberList = Stream.of(3, 5, 1, 4)
.collect(Collectors.toList());
`````

collect로 데이터를 합칠 때 Collectors의 mapping과 reducing를 적용할 수도 있다

mapping : Map과 collect를 합쳐놓은 collector
reducing : reduce를 해주는 collector
````java
List<Integer> numberList = Stream.of(-3, 5, 1, 4)
.collect(Collectors.mapping(x -> Math.abs(x), Collectors.toList());

Integer sum = Stream.of(3, 5, -3, 1)
.collect(Collectors.reducing(0, (x, y) -> x + y));
````
#### toSet
Stream안의 데이터를 Set 형태로 반환해주는 collector
````java
Set<Integer> numberList = Stream.of(3, 5, 1, 3)
.collect(Collectors.toSet());
`````
---
{"dg-publish":true,"permalink":"/공부/Java/Stream/Map/","dgPassFrontmatter":true,"dg-note-properties":{"permalink":"/공부/java/stream/map"}}
---


**데이터를 변형**할 때 사용
데이터에 해당 함수가 적용된 결과물을 제공하는 stream을 리턴한다

````java
List<Integer> ageList = members.stream()
.map(x -> x.getAge())
.collect(Collectors.toList());
````
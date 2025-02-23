---
{"dg-publish":true,"permalink":"//java/stream/collector/to-map/","dgPassFrontmatter":true}
---


---
{"dg-publish":true,"permalink":"/공부/JAVA/Stream/Collector/toMap/","dgPassFrontmatter":true}
---

`Collectors.toMap(keyMapper func, valueMapper func)`
Stream 안의 데이터를 map의 형태로 반환해주는 collector

#### keyMapper
데이터를 map의 key로 변환하는 함수

#### valueMapper
데이터를 map의 value로 변환하는 함수

````java
Map<Integer, Member> memberIdMap = members.stream()
.collect(Collectors.toMap(Member::getId, Member::getName));
`````

valueMapper의 인자로 [[공부/Java/Stream/Function.identity()\|Function.identity()]]를 사용하기도 한다
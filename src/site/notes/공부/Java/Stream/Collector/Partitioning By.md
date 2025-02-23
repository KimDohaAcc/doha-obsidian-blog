---
{"dg-publish":true,"permalink":"/공부/Java/Stream/Collector/Partitioning By/","dgPassFrontmatter":true}
---


[[공부/Java/Stream/Collector/Grouping By\|Grouping By]]와 유사하지만 Function 대신 Predicate를 받아 true와 flase 두 키가 존재하는 map을 반환하는 collector

````java
Map<Boolean, List<Integer>> map = numbers.stream()
.collect(Collectors.partitioningBy(number -> number % 2 == 0));
````
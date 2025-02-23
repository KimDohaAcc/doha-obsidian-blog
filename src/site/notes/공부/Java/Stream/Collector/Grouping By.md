---
{"dg-publish":true,"permalink":"//java/stream/collector/grouping-by/","dgPassFrontmatter":true}
---


Stream 안의 데이터에 classifier를 적용했을 때 **결과값이 같은 값끼리 List로 모아서 Map의 형태로 반환**해주는 collector

이때 key는 classifier의 결과값, value는 데이터들이다

````java
List<Integer> numbers = Arrays.asList(13, 2, 1, 101, 203);

Map<Integer, List<Integer>> map = numbers.stream()
.collect(Collectors.groupingBy(number -> number % 10));

// {1=[1, 101], 2=[2], 3=[13, 203]}
`````
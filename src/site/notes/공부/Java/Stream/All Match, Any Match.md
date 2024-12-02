---
{"dg-publish":true,"permalink":"/공부/JAVA/Stream/All Match, Any Match/","dgPassFrontmatter":true}
---

#### allMatch
Stream 안의 모든 데이터가 predicate를 만족하면 true를 반환

````java
boolean allMatch = numbers.stream()
.allMatch(number -> number > 0);
`````

#### anyMatch
Stream 안의 데이터 중 하나라도 predicate를 만족하면 true를 반환

````java
boolean anyMatch = numbers.stream()
.anyMatch(number -> number > 0);
`````
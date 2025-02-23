---
{"dg-publish":true,"permalink":"//java/stream/distinct/","dgPassFrontmatter":true}
---


---
{"dg-publish":true,"permalink":"/공부/JAVA/Stream/Distinct/","dgPassFrontmatter":true}
---

**중복된 데이터가 제거**된 stream을 리턴

````java
List<String> distinctList = members.stream()
.distinct()
.map(Member::getName)
.collect(Collectors.toList());
`````
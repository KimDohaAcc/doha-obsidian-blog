---
{"dg-publish":true,"permalink":"//java/stream/filter/","dgPassFrontmatter":true}
---


---
{"dg-publish":true,"permalink":"/공부/JAVA/Stream/Filter/","dgPassFrontmatter":true}
---

**특정 조건을 만족하는 데이터**만 걸러내는 데 사용
조건식에 true를 반환하는 데이터만 존재하는 stream을 리턴한다

````java
List<Member> ageFilteredList = members.stream()
.filter(x -> x.getAge() > 30)
.collect(Collectors.toList());
````
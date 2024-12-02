---
{"dg-publish":true,"permalink":"/공부/JAVA/Stream/Sorted/","dgPassFrontmatter":true}
---

**데이터가 순서대로 정렬**된 stream을 반환
데이터의 종류에 따라 Comparator가 필요할 수 있다

데이터를 이름순으로 오름차순 정렬 후 이름 목록을 출력
````java
List<String> nameAscList = members.stream()
.sorted((o1, o2 -> o1.getName().compareTo(o2.getName()))
	   .map(Member::getName)
	   .collect(Collectors.toList());
````
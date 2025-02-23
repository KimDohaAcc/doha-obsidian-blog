---
{"dg-publish":true,"permalink":"//java/stream/function-identity/","dgPassFrontmatter":true}
---


---
{"dg-publish":true,"permalink":"/공부/JAVA/Stream/Function.identity()/","dgPassFrontmatter":true}
---

값을 그대로 반환하는 항등 함수
`Map<Integer, Member> memberIdMap = members.stream() .collect(Collectors.toMap(Member::getId, Function.identity())`
이렇게 사용한다면 member 객체 자체가 값이 되도록 매핑하는 것이다
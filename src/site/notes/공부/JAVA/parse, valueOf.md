---
{"dg-publish":true,"permalink":"/공부/JAVA/parse, valueOf/","dgPassFrontmatter":true}
---

#### parse

`타입.parse타입(String s)`의 형식을 갖는다

대표적으로 Integer.paseInt(), Long.parseLong() 등이 있다.
이는 *문자열 -> primitive 타입*으로 바꿔준다
그래서 Integer.paseInt("100")을 하면 **int형 100**이 반환된다

#### valueOf

`타입.valueOf(String s)`의 형식을 갖는다

대표적으로 Integer.valueOf(), Double.valueOf() 등이 있다.
이는 *문자열 -> wrapper 클래스 타입*으로 바꿔준다
그래서 Integer.valueOf("100")을 하면 **Integer 객체 100**이 반환된다
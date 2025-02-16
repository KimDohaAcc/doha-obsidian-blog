---
{"dg-publish":true,"permalink":"/공부/JAVA/switch/","dgPassFrontmatter":true}
---

case를 나눠서 작성할 때 모든 case마다 break 가 붙는다면, 람다식으로 작성할 수 있다(java 12)

````java
switch(input) {
	case "1" -> System.out.println(1);
	case "2" -> System.out.println(2);
	case "3" -> System.out.println(3);
}
````
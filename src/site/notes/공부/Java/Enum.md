---
{"dg-publish":true,"permalink":"/공부/Java/Enum/","dgPassFrontmatter":true}
---


상수의 그룹을 나타낼 때 사용
JDK 1.5 이상의 버전에서만 사용 가능하다
#### 사용

````java
public enum Role { 
	USER, ADMIN; 
}
````

**[[공부/JPA/Annotation/@Enumerated\|@Enumerated]]** 어노테이션을 이용하면 EnumType을 사용할 수 있다
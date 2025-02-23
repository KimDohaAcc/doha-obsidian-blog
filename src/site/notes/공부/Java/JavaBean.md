---
{"dg-publish":true,"permalink":"//java/java-bean/","dgPassFrontmatter":true}
---


아래 두 가지 관례를 따라 만들어진 오브젝트를 자바빈, 혹은 빈이라고 부른다.

1. 디폴트 생성자 - 파라미터 없는 디폴트 생성자. 툴이나 프레임워크에서 [[공부/Language/리플렉션(Reflection)\|리플렉션(Reflection)]]을 이용해 객체를 생성하기 때문
3. 프로퍼티 - 자바빈이 노출하는 이름을 가진 속성을 프로퍼티라 한다. set 수정자와 getter 접근자가 있다

###### 예시

```java
public class User {
	String id;
	String name;
	String password;
	
	public String getId() {
		return id;
	}

	public void setId(String id) {
		this.id = id;
	}

	public String getName() {
		return name;
	}
}
```
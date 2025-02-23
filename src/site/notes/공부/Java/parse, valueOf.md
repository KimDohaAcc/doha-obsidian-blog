---
{"dg-publish":true,"permalink":"//java/parse-value-of/","dgPassFrontmatter":true}
---


---
dg-publish: true
---
#### parse

`타입.parse타입(String s)`의 형식을 갖는다

대표적으로 Integer.paseInt(), Long.parseLong() 등이 있다.
이는 *문자열 -> primitive 타입*으로 바꿔준다
그래서 Integer.paseInt("100")을 하면 **int형 100**이 반환된다

#### valueOf

`타입.valueOf(String s)`의 형식을 갖는다

대표적으로 Integer.valueOf(), Double.valueOf() 등이 있다.
이는 *문자열 -> [[공부/Java/Wrapper Class\|Wrapper Class]] 타입*으로 바꿔준다
그래서 Integer.valueOf("100")을 하면 **Integer 객체 100**이 반환된다

#### autoboxing

JDK 1.5부터 도입된 오토박싱 기능 때문에 반환값이 기본형일 때와 wrapper 클래스일 때 차이가 사라졌다

즉 Integer.valueOf()로 Integer 객체가 반환되더라도 변수가 int 형이라면 오토박싱으로 int로 변환된다. 그리고 변환은 물론 참조형 간의 연산도 가능하다.

하지만 Java의 원리가 바뀐 것이 아니라 컴파일러가 제공하는 편리한 기능임에 유의하자
간략하게 `Integer a = (int) i`라고 쓴 구문을 컴파일러가 원래 구문인 `Integer a = Integer.valueOf(i)`로 변경해주는 것일 뿐이다.
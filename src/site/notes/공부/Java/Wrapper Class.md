---
{"dg-publish":true,"permalink":"//java/wrapper-class/","dgPassFrontmatter":true}
---


---
dg-publish: true
---
기본형 변수를 ==객체로 다루는 클래스==
[[공부/Java/변수(variable)/변수의 타입\|변수의 타입]] 중 primitive type 변수를 객체로 다뤄야 하는 상황에 사용할 수 있다

8개의 기본형과 마찬가지로 8개의 Wrapper Class가 존재한다

##### 객체로 다뤄야 할 상황?

예를 들면 매개변수로 객체를 요구하거나,
기본형 값이 아닌 객체로 저장해야 할 때,
객체 간의 비교가 필요할 때 등의 상황에서 기본형 값을 객체로 변환해 작업을 처리해야 한다

##### 종류
boolean - Boolean
char - Character
byte - Byte
short - Short
int - Integer
long - Long
float - Float
double - Double

##### 메소드

wrapper 클래스는 모두 equals(), toString()이 오버라이딩 되어있다.
equals로는 객체의 값을 비교할 수 있으며, toString은 주솟값이 아닌 값을 출력한다

그 외에도 MAX_VALUE, MIN_VALUE, SIZE, BYTE 등의 static 멤버를 공통으로 가지고 있다
예를 들어 `Integer.SIZE`는 32이다


##### 문자열 -> wrapper class 변환 방법

[[공부/Java/parse, valueOf\|parse, valueOf]] 중 **valueOf**를 사용해 문자열을 wrapper class로 변환할 수 있다
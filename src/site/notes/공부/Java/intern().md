---
{"dg-publish":true,"permalink":"//java/intern/","dgPassFrontmatter":true}
---


문자열을 [[공부/Java/String Constant Pool\|String Constant Pool]]에 넣어주는 메소드

리터럴로 선언된 문자열은 런타임 시 스캔 대상이 되어 String Constant Pool에 저장되지만,
new String("...")으로 선언된 문자열은 상수풀이 아닌 [[공부/Java/힙(Heap) 메모리\|힙(Heap) 메모리]]에 올라가게 된다

*이때 intern() 메소드를 사용하면 강제로 String Constant Pool에 넣어줄 수 있다*

이미 해당 문자열이 String Constant Pool에 들어있다면 넣지 않고, 없다면 강제로 저장한다
return 값은 상수풀에 있는 레퍼런스 값이다

어지간하면 사용할 일도 없고, 사용하지 않는 것이 좋다
String Constant Pool은 [[공부/Java/가비지 콜렉터(Garbage Collector, GC)\|가비지 콜렉터(Garbage Collector, GC)]]의 대상이 되지 않고 애플리케이션 종료 시까지 메모리에 남아있기 때문에 ==메모리 누수== 가능성을 높인다

#### 실행 예시
```java
new String("Hello World").intern(); // String pool에 강제로 넣음
new String("World").intern(); // String pool에 강제로 넣음
new String("Hello World").intern(); // 이미 String pool에 있기 때문에, 추가되지 않음
```
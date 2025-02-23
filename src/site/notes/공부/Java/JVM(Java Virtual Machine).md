---
{"dg-publish":true,"permalink":"//java/jvm-java-virtual-machine/","dgPassFrontmatter":true}
---


한마디로 정리하면 '[[공부/Java/자바(Java Programming Language)\|자바(Java Programming Language)]]를 실행하기 위한 가상 기계(컴퓨터)' 라고 할 수 있다

#### 가상 기계(Virtual machine)
넓은 의미에서 소프트웨어로 구현된 하드웨어를 뜻한다. 예시로는 TV와 비디오를 소프트웨어화 한 윈도우 미디어 플레이어 등이 있다.

좁은 의미에서는 '가상 컴퓨터'를 가리키는데, 실제 컴퓨터(하드웨어)가 아닌 소프트웨어로 구현된 컴퓨터라는 뜻이다.

자바로 작성된 애플리케이션은 모두 가상 컴퓨터인 JVM에서만 실행된다

hardware <-> OS <-> JVM <-> Java Application

### 운영체제에 종속적
Java는 운영체제에 독립적이지만, JVM은 해당 OS에서 실행가능한 버전이 필요하다
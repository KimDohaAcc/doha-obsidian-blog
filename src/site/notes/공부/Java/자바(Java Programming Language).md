---
{"dg-publish":true,"permalink":"//java/java-programming-language/","dgPassFrontmatter":true}
---


---
dg-publish: true
---
자바는 썬 마이크로시스템즈(Sun Microsystems)에서 개발하여 1996년 1월에 공식적으로 발표한 *객체지향 프로그래밍 언어*이다

연산자와 기본 구문은 [[공부/Language/C++\|C++]]에서, 객체 지향 관련 구문은 스몰톡이라는 객체 지향 언어에서 가져왔다

#### 특징

==운영체제에 독립적==
자바로 작성된 프로그램은 운영체제의 종류에 관계 없이 실행이 가능하다
자바 응용프로그램은 운영체제나 하드웨어가 아닌 **JVM**하고만 통신하며, JVM이 자바 응용프로그램으로부터 전달 받은 명령을 해당 운영체제가 이해할 수 있도록 **변환**해 전달한다

그렇기에 자바로 작성된 **프로그램**은 운영체제에 **독립적**이지만, **JVM**은 운영체제에 **종속적**이다
실제로 여러 운영체제에 설치할 수 있는 JVM을 제공하고 있다

==객체 지향 언어==
자바는 [[공부/Language/객체 지향 언어(Object Oriented Programming Language)\|객체 지향 언어(Object Oriented Programming Language)]] 중 하나이다

==자동 메모리 관리(Garbage Collection)==
[[공부/Java/가비지 콜렉터(Garbage Collector, GC)\|가비지 콜렉터(Garbage Collector, GC)]]가 자동적으로 메모리를 관리해주기 때문에 프로그래머는 따로 메모리를 관리할 필요가 없다

==멀티쓰레드 지원==
자바에서 개발되는 멀티쓰레드 프로그램은 운영체제에 관계 없이 구현 가능하다

==동적 로딩(Dynamic Loading) 지원==
자바는 동적 로딩을 지원하기 때문에 실행 시에 모든 클래스가 로딩되지 않고, *필요한 시점에 클래스를 로딩하여 사용할 수 있다*는 장점이 있다
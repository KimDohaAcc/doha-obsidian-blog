---
{"dg-publish":true,"permalink":"/공부/Java/String Constant Pool/","dgPassFrontmatter":true}
---


문자열 리터럴을 저장하는 독립된 영역

String Pool 이라고도 부른다
[[공부/Java/JVM(Java Virtual Machine)\|JVM(Java Virtual Machine)]]의 Perm/Metaspace 영역에 존재하며 일반적으로 GC의 대상이 되지는 않는다

String은 불변 객체이기 때문에 문자열 생성 시 String Constant Pool에 저장된 리터럴을 재사용할 수 있다

#### 저장 위치

![Pasted image 20240821100857.png](/img/user/%EC%B2%A8%EB%B6%80%ED%8C%8C%EC%9D%BC/Pasted%20image%2020240821100857.png)

#### 저장 조건

```java
String str = "Hello world!";  // String constant pool에 저장됨
String doNotUse = new String("Hello World!");  // heap 영역에 저장됨
```

소스코드에 리터럴 형태로 작성한 문자열이 String Constant Pool 저장 대상이 된다
컴파일 시 컴파일러에 의해 저장 대상으로 표시된다
`CONSTANT_String` 타입으로 표시되기 때문에 런타임 시 스캔 대상이 되어 String Constant Pool로 저장을 하게 된다

이렇게 String Constant Pool에 저장된 문자열은 모두 *같은 객체를 재사용*한다
그래서 같은 리터럴로 선언된 문자열은 같은 값을 갖는다

```java
String str = "hello"; // String constant pool에 저장
String str2 = "hello"; // String constant pool에서 재사용
String str3 = new ("hello"); // 별도의 Heap 메모리에 저장

System.out.println(str == str2);	// true (같은 객체를 재사용하기 때문에)
System.out.println(str == str3);	// false
System.out.println(str.equals(str3));	// true
```
![Pasted image 20240821100807.png](/img/user/%EC%B2%A8%EB%B6%80%ED%8C%8C%EC%9D%BC/Pasted%20image%2020240821100807.png)
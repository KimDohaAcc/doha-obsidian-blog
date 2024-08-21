---
{"dg-publish":true,"permalink":"/공부/JAVA/Constant Pool(Class file Constant Pool)/","dgPassFrontmatter":true}
---

컴파일 시 ==클래스 파일 내부==에 존재하는 영역
클래스로더에 의해 [[공부/JAVA/JVM(Java Virtual Machine)\|JVM(Java Virtual Machine)]]에 로드될 때 메모리에 로드한다

주로 *클래스 구성요소(상수, 문자열, 클래스/인터페이스 참조) 데이터*를 저장하고 있다

#### 구성

```java
class Hello {
    public static void main( String[] args ) {
        for( int i = 0; i < 10; i++ )
            System.out.println( "Hello from Hello.main!" );
  }
}
```

이런 클래스 파일을 컴파일 한 후 상수풀을 열어보면 다음과 같이 되어 있다
```
  #1 = Methodref          #6.#16         // java/lang/Object."<init>":()V
   #2 = Fieldref           #17.#18        // java/lang/System.out:Ljava/io/PrintStream;
   #3 = String             #19            // Hello from Hello.main!
   #4 = Methodref          #20.#21        // java/io/PrintStream.println:(Ljava/lang/String;)V
   #5 = Class              #22            // Hello
   #6 = Class              #23            // java/lang/Object
   #7 = Utf8               <init>
   #8 = Utf8               ()V
   #9 = Utf8               Code
  #10 = Utf8               LineNumberTable
  #11 = Utf8               main
  #12 = Utf8               ([Ljava/lang/String;)V
  #13 = Utf8               StackMapTable
  #14 = Utf8               SourceFile
  #15 = Utf8               Hello.java
  #16 = NameAndType        #7:#8          // "<init>":()V
  #17 = Class              #24            // java/lang/System
  #18 = NameAndType        #25:#26        // out:Ljava/io/PrintStream;
  #19 = Utf8               Hello from Hello.main!
  #20 = Class              #27            // java/io/PrintStream
  #21 = NameAndType        #28:#29        // println:(Ljava/lang/String;)V
  #22 = Utf8               Hello
  #23 = Utf8               java/lang/Object
  #24 = Utf8               java/lang/System
  #25 = Utf8               out
  #26 = Utf8               Ljava/io/PrintStream;
  #27 = Utf8               java/io/PrintStream
  #28 = Utf8               println
  #29 = Utf8               (Ljava/lang/String;)V
```

`
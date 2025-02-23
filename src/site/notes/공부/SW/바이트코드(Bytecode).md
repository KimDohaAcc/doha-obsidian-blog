---
{"dg-publish":true,"permalink":"/공부/SW/바이트코드(Bytecode)/","dgPassFrontmatter":true}
---


프로그래밍 언어와 기계어 사이의 ==중간 단계 코드==
특정 하드웨어가 아닌 **가상 컴퓨터**에서 돌아가 실행 프로그램을 위한 **이진 표현법**이다

1바이트 크기의 명령어로 구성되어 있어서 바이트코드라고 불리게 됐다

#### 정의
고급 프로그래밍 언어로 작성된 소스 코드를 컴파일한 결과물
가상 머신이나 인터프리터가 실행할 수 있는 형태이다

#### 목적
플랫폼 독립성을 제공하고, 실행 속도를 향상시키며, 코드 최적화를 가능하게 한다

#### 사용처
[[공부/Java/자바(Java Programming Language)\|자바(Java Programming Language)]]의 [[`.class`]]
Python의 .pyc

#### 사용 예시

###### Java
```java
public class HelloWorld { public static void main(String[] args) { System.out.println("Hello, World!"); } }
```
이 코드를 컴파일하면 HelloWorld.class 파일이 생성되며, 바이트 코드를 포함하고 있다

`javap -c HelloWorld.class` 명령어로 확인할 수 있다
[[공부/Java/JDK(Java Development Kit)\|JDK(Java Development Kit)]] 중 javap.exe 는 클래스 파일을 원래 소스로 변환하는 역어셈블러다.

```bytecode
public class HelloWorld {
  public static void main(java.lang.String[]);
    Code:
       0: getstatic     #7                  // Field java/lang/System.out:Ljava/io/PrintStream;
       3: ldc           #13                 // String Hello, World!
       5: invokevirtual #15                 // Method java/io/PrintStream.println:(Ljava/lang/String;)V
       8: return
}
```

이러한 Java 바이트코드가 JVM에서 실행된다

###### Python
```python
def greet(name):
    return f"Hello, {name}!"

print(greet("World"))
```
Python은 이 코드를 실행할 때 자동으로 바이트코드로 컴파일한다.

`dis.dis(greet)`
.pyc 파일에 저장되는 바이트코드는 dis 모듈을 사용해서 확인할 수 있다

``` bytecode
2           0 LOAD_CONST               1 ('Hello, ')
              2 LOAD_FAST                0 (name)
              4 FORMAT_VALUE             0
              6 BUILD_STRING             2
              8 RETURN_VALUE
```

이러한 Python 바이트코드가 Python Virtual Machine에서 실행된다

#### 장점
플랫폼 간 이식성이 높다
소스 코드를 보호한다
실행 속도를 향상시킨다

#### 단점
네이티브 코드에 비해 실행 속도가 다소 느릴 수 있다
가상 머신 등 추가적인 실행 환경이 필요하다
---
{"dg-publish":true,"permalink":"/정보처리기사 실기/프로그래밍 기출(2017~2023)/2023 3회/기출문제 - Java/","dgPassFrontmatter":true}
---

```java
다음은 Java 코드이다. 올바른 출력 결과를 쓰시오.

​

public class Soojebi {

  public static void main(String[] args) {

    A b = new B();

    b.paint();

    b.draw();

  }

}

class A {

  public void paint() {

    System.out.print("A");

    draw();

  }

  public void draw() {

    System.out.print("B");

    draw();

  }

}

class B extends A {

  public void paint() {

    super.draw();

    System.out.print("C");

    this.draw();

  }

  public void draw() {

    System.out.print("D");

  }

}

```


#### 정답
BDCDD

#### 풀이


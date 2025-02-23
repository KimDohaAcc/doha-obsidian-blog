---
{"dg-publish":true,"permalink":"////singleton/","dgPassFrontmatter":true}
---


객체의 인스턴스를 한개만 생성되게 하는 [[공부/디자인 패턴/생성 패턴/생성 패턴\|생성 패턴]]의 일종
#### 싱글톤 패턴을 사용하는 이유

**1. 메모리 측면의 이점**  
싱글톤 패턴을 사용하게 된다면 한개의 인스턴스만을 고정 메모리 영역에 생성하고 추후 해당 객체를 접근할 때 메모리 낭비를 방지할 수 있다.

**2. 속도 측면의 이점**  
생성된 인스턴스를 사용할 때는 이미 생성된 인스턴스를 활용하여 속도 측면에 이점이 있다.

**3. 데이터 공유가 쉽다**  
전역으로 사용하는 인스턴스이기 때문에 다른 여러 클래스에서 데이터를 공유하며 사용할 수 있다. 하지만 동시성 문제가 발생할 수 있어 이 점은 유의하여 설계하여야 한다.

#### 싱글톤 패턴 구현

```java
public class Singleton {
    // 단 1개만 존재해야 하는 객체의 인스턴스로 static 으로 선언
    private static Singleton instance;

    // private 생성자로 외부에서 객체 생성을 막아야 한다.
    private Singleton() {
    }

    // 외부에서는 getInstance() 로 instance 를 반환
    public static Singleton getInstance() {
        // instance 가 null 일 때만 생성
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
```
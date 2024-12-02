---
{"dg-publish":true,"permalink":"/공부/Java/댕글링 포인터(Dangling Pointer)/","dgPassFrontmatter":true}
---


**이미 해제된 메모리를 가리키는 포인터**를 의미

주로 수동 메모리 관리를 사용하는 언어(C, C++)에서 문제가 발생한다

#### 댕글링 포인터 문제
해제된 메모리에 접근하여 예측 불가능한 동작이나 프로그램 충돌을 일으키는 문제
보안 취약점의 원인이 될 수 있다

#### 가비지 컬렉터의 해결 방식
[[공부/Java/가비지 콜렉터(Garbage Collector, GC)\|가비지 컬렉터(Garbage Collector, GC)]]는 자동으로 사용하지 않는 메모리를 식별하고 해제한다
또한, 객체가 여전히 참조되고 있다면 메모리를 해제하지 않는다

==해제된 메모리에 대한 접근을 방지==한다. 예를 들어 객체 참조가 null일 경우 NullPointerException을 발생시키는 등 접근을 방지함으로써 ==안정성과 보안을 향상==한다
###### Java에서의 예시
```java
public class DanglingPointerExample {
    public static void main(String[] args) {
        Object obj = new Object();
        // obj는 유효한 객체를 참조

        obj = null;
        // obj는 더 이상 객체를 참조하지 않음
        // 가비지 컬렉터가 이전 객체를 자동으로 수거할 것임

        // Java에서는 null인 obj를 사용하려 하면 NullPointerException 발생
        // System.out.println(obj.toString()); // 이 라인은 예외를 발생시킴
    }
}
```

###### C/C++ 에서의 댕글링 포인터 문제 예시
```c
#include <stdlib.h>

int main() {
    int* ptr = (int*)malloc(sizeof(int));
    *ptr = 10;
    
    free(ptr);  // 메모리 해제
    
    // 댕글링 포인터 문제: ptr은 여전히 해제된 메모리를 가리킴
    *ptr = 20;  // 위험한 동작: 정의되지 않은 행동
    
    return 0;
}
```
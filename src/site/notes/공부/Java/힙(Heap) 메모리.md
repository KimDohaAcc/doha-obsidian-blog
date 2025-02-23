---
{"dg-publish":true,"permalink":"//java/heap/","dgPassFrontmatter":true}
---


**동적으로 할당되고 해제**할 수 있는 메모리 영역
new 로 할당할 수 있다

JVM 옵션에서 초기 힙 크기, 최대 힙 크기를  설정할 수 있다
==런타임==에 크기가 결정된다. Java에서는 [[공부/Java/가비지 콜렉터(Garbage Collector, GC)\|가비지 컬렉터(Garbage Collector, GC)]]가 힙 영역의 메모리를 관리한다.

#### 구조
- Young Generation : 새로 생성된 객체와 Minor GC 후 살아남은 객체들이 존재
- Old Generation : 오래 살아남은 객체들이 위치함
###### 예시

```java
public class HeapExample {
    public static void main(String[] args) {
        // 사용자 입력에 따라 리스트 크기가 달라질 수 있음
        Scanner scanner = new Scanner(System.in);
        System.out.print("리스트 크기를 입력하세요: ");
        int size = scanner.nextInt();

        // 런타임에 결정된 크기로 ArrayList 생성
        ArrayList<Integer> list = new ArrayList<>();
        for (int i = 0; i < size; i++) {
            list.add(i);
        }

        System.out.println("리스트 크기: " + list.size());
    }
}
```

이 예시에서 사용자의 입력에 따라 ArrayList의 크기가 결정되고, 프로그램 종료 후 이 메모리는 운영체제에 반환된다
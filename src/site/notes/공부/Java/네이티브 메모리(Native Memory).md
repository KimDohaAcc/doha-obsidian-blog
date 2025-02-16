---
dg-publish: true
---
[[공부/Java/JVM(Java Virtual Machine)\|JVM(Java Virtual Machine)]] 힙 외부에 있는 메모리
운영체제가 직접 할당하고 관리한다
그렇기 때문에 [[공부/Java/가비지 콜렉터(Garbage Collector, GC)\|가비지 콜렉터(Garbage Collector, GC)]] 관리 대상이 아니다

개발자나 JVM이 명시적으로 메모리를 할당 및  해제해야 한다
[[공부/Java/힙(Heap) 메모리\|힙(Heap) 메모리]] 크기 제한에 영향이 없고 가비지 컬렉션 오버헤드가 없다

힙 메모리에 비해서는 상세한 분석이 어렵다
#### 예시
JNI(Java Native Interface)를 통해 호출되는 네이티브 코드
일부  Java 라이브러리의 내부 구현
JVM 자체의 내부 데이터 구조
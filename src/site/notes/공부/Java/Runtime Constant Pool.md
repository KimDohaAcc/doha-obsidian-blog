---
{"dg-publish":true,"permalink":"/공부/Java/Runtime Constant Pool/","dgPassFrontmatter":true}
---


상수 풀이라고도 부른다
Java 8 이전에는 [[공부/Java/JVM(Java Virtual Machine)\|JVM(Java Virtual Machine)]]- Perm 영역에 저장되었고, 이후부터는 JVM - Metaspace 영역에 저장된다

[[공부/Java/Constant Pool(Class file Constant Pool)\|Constant Pool(Class file Constant Pool)]]이 런타임 시 이 영역으로 저장된다

주로 *클래스/인터페이스의 상수 정보*(리터럴 상수, 타입, 필드, 메소드)를 저정한다

클래스 상수 풀 또한 클래스로더에 의해 클래스를 로딩할 때 Runtime Constant Pool에 저장된다

### Perm(Permanent Generation) -> Metaspace

Perm : [[공부/Java/힙(Heap) 메모리\|힙(Heap) 메모리]]영역의 일부
Metaspace : [[공부/Java/네이티브 메모리(Native Memory)\|네이티브 메모리(Native Memory)]](OS에서 관리하는 메모리)

Perm 영역에 데이터가 저장될 때는 클래스, Metadata 로딩 과정에서 메모리 누수가 발생했다
또한 Perm 영역의 크기를 고정적으로 설정해야 해 메모리 부족으로 Out Of Memory Error가 발생하는 일이 있었다

이를 개선하기 위해 Constant Pool을 ==Metaspace 영역으로 이관==했다

Metaspace 영역은 JVM의 Native Memory를 사용하며 JVM이 관리하기 때문에 메모리가 동적으로 관리되며 필요한 경우 OS에게 요청해 메모리를 추가 할당할 수 있다

이관하며 클래스 로딩이 많은 애플리케이션에서 이점을 보게 되었다

#### 궁금증

떠오르는 몇 가지 질문을 해소하고 가도록 하자

###### 메모리는 계속 확장되나?

Metaspace는 필요에 따라 *자동으로 확장*되므로, 제한을 두지 않으면 과도한 메모리 사용이 발생할 수 있다
MaxMetaspaceSize 라는 옵션이 있어 상한선을 설정할 수 있다고 한다

###### Metaspace의 메모리 관리는 어떻게 이루어지나?

Metaspace는 클래스로더 단위로 메모리를 관리한다. Metaspace는 클래스 로더별로 메모리 블록을 할당하며, 각 블록은 여러 개의 클래스 메터데이터를 저장할 수 있는 크기로 설게된다.[^JEP_122:Remove_the_Permanent_Generation] 
물론 더 많은 클래스를 로드하면 동적으로 블록이 할당된다.

클래스 로더가 소멸될 때, 해당 클래스 로더와 연관된 모든 블록이 한 번에 해제된다. 이를 통해 메모리 관리를 효율적으로 하고, 클래스 로더가 소멸될 때 관련 모든 메모리를 한 번에 해제할 수 있어 **메모리 누수 위험이 감소**한다.

그러나 부적절한 클래스 로더 사용으로 인한 누수 문제는 남아있기 때문에, 클래스 로더를 올바르게 사용해야 한다

###### Metaspace에서의 GC?

Metaspace는 [[공부/Java/가비지 콜렉터(Garbage Collector, GC)\|가비지 콜렉터(Garbage Collector, GC)]] 기능을 가지고 있어서, 용량이 가득 찼을 때 더 이상 사용하지 않는 클래스 메터데이터들을 제거한다.

이때 GC의 대상이 되는 메타데이터는, 자신을 로드한 클래스로더가 힙 메모리에서 GC된 것들이다.
즉, 자신을 로드한 클래스로더가 힙에 살아있으면 GC 되지 않는다. 이 때문에 클래스로더 메모리 누수 문제가 발생할 수 있다.

![Pasted image 20240821112830.png](/img/user/%EC%B2%A8%EB%B6%80%ED%8C%8C%EC%9D%BC/Pasted%20image%2020240821112830.png)
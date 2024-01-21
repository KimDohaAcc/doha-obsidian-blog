---
{"dg-publish":true,"permalink":"/공부/SW/자료구조/ArrayDeque/","dgPassFrontmatter":true}
---

Deque interface의 ==사이즈 조정이 가능한 array의 구현체==

 [[공부/SW/자료구조/Stack\|Stack]]으로 쓸 때 Stack 보다는 빠르고, [[공부/SW/자료구조/Queue\|Queue]]로 쓸 때 [[공부/SW/자료구조/리스트/LinkedList\|LinkedList]]보다 빠르다
 
==크기를 재설정== 할 수 있다

#### Stack보다 빠른 이유
Stack은 모든 메소드에 synchromized가 있어 단일 스레드 환경에서 성능이 떨어지며, Vector 클래스를 상속받았기 때문에 LIFO 구조를 유지하는 것이 아니라 중간에서 데이터를 삭제하고 삽입하는 것이 가능하다. 또한 초기 용량을 설정할 수 없다.

-> 위와 같은 문제를 ArrayDeque 를 사용하면 해결이 되며 쓰레드 safe 하게 설계할 수 있다

#### LinkedList와 비교

ArrayDeque와 LinkedList 는 모두 Deque 인터페이스의 구현체이다
ArrayDeque는 대기열 작업에 더 효율적이고, LinkedList는 목록 중간에 있는 작업에 대해 더 나은 성능을 제공한다
LinkedList는 null을 추가할 수 있지만, ArrayDeque는 불가능하다
LinkedList는 반복 중에 현재 요소를 제거하는 것에 효율적이고, ArrayDeque는 양쪽 끝에서 추가, 제거가 효율적이다
Array는 LinkedList보다 cache-locality 친화적이다
LinkedList는 이전 및 다음 포인터의 저장으로 인해 추가 메모리 오버헤드가 있다
ArrayDeque는 다음 노드에 추가적인 reference를 유지할 필요가 없기 때문에 LinkedList보다 메모리 효율적이다
### 언제 어떤 걸 써야 할까?
1. Queue가 필요한 경우 Deque를 사용해라
2. 대부분의 상황에선 구현체로는 LinkedList 보단 ArrayDeque를 사용해라
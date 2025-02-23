---
{"dg-publish":true,"permalink":"///array-deque/","dgPassFrontmatter":true}
---


---
{"dg-publish":true,"permalink":"/공부/SW/자료구조/ArrayDeque/","dgPassFrontmatter":true}
---

Deque interface의 ==사이즈 조정이 가능한 array의 구현체==

 [[공부/자료구조/Stack\|Stack]]으로 쓸 때 Stack 보다는 빠르고, [[공부/자료구조/Queue\|Queue]]로 쓸 때 [[공부/자료구조/리스트/LinkedList\|LinkedList]]보다 빠르다
 
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

LinkedList는 요소를 추가하거나 제거할 때 단순히 노드를 연결하거나 끊으면 돼서 크기 변경에 따른 추가적인 연산이 없지만, ArrayDeque는 내부 배열이 가득 차면 더 큰 배열을 새로 할당하고 모든 요소를 복사해야 해서 시간이 더 걸릴 수 있다.

queue의 크기가 자주 변한다면 LinkedList는 크기 변경에 따른 추가적인 메모리 할당이나 복사 작업이 필요가 없어서 효율적일 수 있다

또한 LinkedList는 요소가 제거될 때 해당 노드 객체가 바로 가비지 컬렉션의 대상이 되지만, ArrayDeque는 내부 배열의 크기가 줄어들지 않아 사용하지 않는 메모리를 계속 유지할 수 있다. 결론적으로, 특정 문제에서는 큐의 크기가 자주 변하고 대규모 데이터를 다룬다면 LinkedList의 유연한 메모리 관리가 유리하게 작용할 수 있다.

Java에서 ArrayDequeue는 기본 초기 용량이 16이다. 요소의 수가 배열 길이 -1 개가 되면 이전 크기의 2배로 재할당 되는데 O(n)시간이 걸린다

**BFS에서 LinkedList가 더 효율적일 수 있는 경우:**

1. 그래프의 구조가 매우 불규칙하여 큐의 크기가 급격하게 변할 때
2. 메모리 할당/해제가 빈번하게 일어나는 환경에서
3. 큐의 최대 크기가 매우 클 때 (ArrayDeque의 재할당 비용이 커질 수 있음)

**그러나 대부분의 BFS 상황에서는 ArrayDeque가 더 효율적일 가능성이 높다:**

1. BFS는 보통 한 번에 모든 노드를 방문하지 않으므로, 급격한 큐 크기 변화가 덜 발생합니다.
2. ArrayDeque의 캐시 효율성이 전체 성능에 긍정적인 영향을 미칩니다.
3. 대부분의 BFS 구현에서 큐 크기가 그래프의 전체 노드 수를 넘지 않아, 재할당이 제한적입니다.
### 언제 어떤 걸 써야 할까?
1. Queue가 필요한 경우 Deque를 사용해라
2. 대부분의 상황에선 구현체로는 LinkedList 보단 ArrayDeque를 사용해라
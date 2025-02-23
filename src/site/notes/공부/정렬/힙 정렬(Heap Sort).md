---
{"dg-publish":true,"permalink":"///heap-sort/","dgPassFrontmatter":true}
---


---
dg-publish: true
---
![heapsort.gif](/img/user/%EC%B2%A8%EB%B6%80%ED%8C%8C%EC%9D%BC/heapsort.gif)

[[공부/자료구조/트리/최대 힙(Max Heap)\|최대 힙(Max Heap)]]혹은 [[공부/자료구조/트리/최소 힙(Min Heap)\|최소 힙(Min Heap)]]을 구성하여 정렬하는 방식이다

1) 입력으로 들어오는 배열로 [[공부/자료구조/트리/힙(Heap)\|힙(Heap)]] 트리를 만든다
2) 내림차순 정렬의 경우 최대 힙 트리를, 오름차순 정렬의 경우 최소 힙 트리를 구성한다
3) 힙 트리로 구한 최댓값 혹은 최솟값에 해당하는 root를 빼내서 배열에 할당한다
4) 하나씩 빼낸 root 노드 자리에는 힙트리 가장 뒤에 있는 원소를 넣는다

힙 정렬은 여러 개의 값 중에서 **최댓값**이나 **최솟값**을 빠르게 찾기 위해 사용된다

#### 시간복잡도
최선, 평균, 최악 모두 **O(NlogN)**이다

#### 특징
- 가장 크거나 가장 작은 값을 구할 때 유용하다
- 멀리 떨어진 요소를 정렬할 때 유용하다(삽입정렬보다 개선된 결과)
- 항상 같은 시간 복잡도를 가지기 때문에 성능이 준수하다
- 주어진 배열 내부에서 위치를 바꾸는 방식으로 하면 [[공부/정렬/제자리 정렬(Inplace algorithm)\|제자리 정렬(Inplace algorithm)]]이 가능하다
- 같은 시간복잡도 O(NlogN)을 가지는 다른 정렬 알고리즘과 비교하면 ==느리다== ([[공부/정렬/퀵 정렬(Quick Sort)\|퀵 정렬(Quick Sort)]]과 [[공부/정렬/병합 정렬(Merge sort)\|병합 정렬(Merge sort)]]의 성능이 좋기 떄문에 힙 정렬 사용빈도는 높지 않다)
- [[공부/정렬/불안정 정렬(Unstable Sort)\|불안정 정렬(Unstable Sort)]]이다

## 코드
```javascript
class Heap {
  constructor() {
    this.heap = [];
  }

  getLeftChild = (parent) => {
    return parent * 2 + 1;
  };

  getRightChild = (parent) => {
    return parent * 2 + 2;
  };

  getParent = (child) => {
    return Math.floor((child - 1) / 2);
  };

  insert = (key, value) => {
    const node = { key, value };
    this.heap.push(node);
    this.heapifyUp();
  };

  remove = () => {
    const count = this.heap.length;
    const root = this.heap[0];

    if (count <= 0) return;

    if (count === 1) {
      this.heap = [];
    } else {
      this.heap[0] = this.heap.pop();
      this.heapifyDown();
    }

    return root;
  };

  heapifyUp = () => {
    let index = this.heap.length - 1;
    const insertedNode = this.heap[index];

    while (index > 0) {
      const parent = this.getParent(index);

      if (this.heap[parent].key > insertedNode.key) {
        this.heap[index] = this.heap[parent];
        index = parent;
      } else {
        break;
      }
    }

    this.heap[index] = insertedNode;
  };

  heapifyDown = () => {
    let index = 0;
    const count = this.heap.length;
    const root = this.heap[index];

    while (this.getLeftChild(index) < count) {
      const leftChild = this.getLeftChild(index);
      const rightChild = this.getRightChild(index);

      let minChild;

      if (
        rightChild < count &&
        this.heap[rightChild].key < this.heap[leftChild].key
      ) {
        minChild = rightChild;
      } else {
        minChild = leftChild;
      }

      if (this.heap[minChild].key <= root.key) {
        this.heap[index] = this.heap[minChild];
        index = minChild;
      } else {
        break;
      }
    }

    this.heap[index] = root;
  };
}

function heapSort(arr) {
  const heap = new Heap();

  for (const element of arr) {
    heap.insert(element);
  }

  const sorted = [];

  while (heap.heap.length) {
    const { key } = heap.remove();
    sorted.push(key);
  }

  return sorted;
}
```
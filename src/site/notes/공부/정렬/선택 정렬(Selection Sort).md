---
{"dg-publish":true,"permalink":"/공부/정렬/선택 정렬(Selection Sort)/","dgPassFrontmatter":true}
---

![image 2.gif](/img/user/%EC%B2%A8%EB%B6%80%ED%8C%8C%EC%9D%BC/image%202.gif)
배열에서 가장 작은 값을 찾아 첫 번째 원소와 교환한 후, 그 다음으로 작은 값을 두 번째 원소와 교환하는, ==n번째 작은 값을 선택해 n번째 원소와 교환==하는 방식의 정렬


#### 시간 복잡도
*(n-1) + (n-2) + ... + 2 + 1 = n(n-1)/2* 이므로 **O(n^2)**
배열이 정렬되어 있더라도 확인하기 때문이다

#### 공간 복잡도
주어진 배열 외에 다른 공간이 필요하지 않으므로 **O(N)** 이다

#### 특징
- [[공부/정렬/버블 정렬(Bubble Sort)\|버블 정렬(Bubble Sort)]]과 마찬가지로 구현이 간단하다
- 비교하는 횟수에 비해 교환하는 횟수가 적기 때문에, ==많은 교환이 필요한 자료 상태==에서는 비교적 효율적이다
- 정렬하고자 하는 배열 안에서 교환하는 방식으로 [[공부/정렬/제자리 정렬(Inplace algorithm)\|제자리 정렬(Inplace algorithm)]]이다

#### 단점
데이터를 하나씩 비교하기 때문에 O(n^2)으로 비효율적이다
[[공부/정렬/불안정 정렬(Unstable Sort)\|불안정 정렬(Unstable Sort)]]로 분리된다
정렬된 상태에서 새로운 데이터가 추가되면 효율이 좋지 않다

## 코드
```javascript
function selectionSort(arr) {
  for (let i = 0; i < arr.length; i++) {
    let minIndex = i;
    for (let j = i + 1; j < arr.length; j++) {
      if (arr[minIndex] > arr[j]) {
        minIndex = j;
      }
    }
    const swap = arr[i];
    arr[i] = arr[minIndex];
    arr[minIndex] = swap;
  }
  return arr;
}

const arr = [99, 3, 7, 9, 5, 10, 25, 17];
console.log(selectionSort(arr)); // [3, 5, 7, 9, 10, 17, 25, 99]
```
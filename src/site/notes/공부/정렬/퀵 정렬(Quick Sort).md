---
{"dg-publish":true,"permalink":"/공부/정렬/퀵 정렬(Quick Sort)/","dgPassFrontmatter":true}
---


![quick.gif](/img/user/%EC%B2%A8%EB%B6%80%ED%8C%8C%EC%9D%BC/quick.gif)
[[공부/알고리즘/분할 정복(Divide and Conquer)\|분할 정복(Divide and Conquer)]] 방법을 통한 정렬

하나의 pivot(축)을 정해서 이 pivot보다 ==작은 값은 왼쪽==, ==큰 값은 오른쪽==에 위치시키는 방법이다

1) 왼쪽과 오른쪽에 해당하는 원소들로 두 배열을 나눈다
2) 분할된 두 개의 작은 배열에 대해 *재귀적*으로 반복한다
3) 재귀 호출을 한 번 할 때마다 최소한 하나의 원소는 ==최종 위치가 정해지므로== 모든 위치가 정해지면 끝난다

#### 시간복잡도
최선, 평균의 경우 **O(NlogN)** 이다
최악의 경우 **O(N^2)** 이다 - 이미 정렬이 되어있는 경우

#### 특징
- 한 번 결정된 pivot은 추후 연산에서 제외되기 때문에, 같은 시간복잡도 O(NlogN)을 가지는 다른 정렬 알고리즘 중에 가장 빠르다
- 불필요한 데이터 이동을 줄이고 먼 거리의 데이터를 교환한다
- 정렬된 배열에 대해서는 불균형 분할에 의해 오히려 수행시간이 더 많이 걸린다
- [[공부/정렬/불안정 정렬(Unstable Sort)\|불안정 정렬(Unstable Sort)]]이다

###### 개선 방법
pivot 값이 최솟값 혹은 최댓값으로 지정되어(즉, 이미 정렬되어 있으면) 파티션이 나눠지지 않을 때
배열 가장 앞에 있는 값과 중간값을 교환하여 중간값이 *pivot*이 되도록 하면 확률적으로나마 시간복잡도를 O(N^2)에서 ==O(NlogN)==으로 개선할 수 있다

## 코드
```javascript
function quickSort(arr) {
  if (arr.length <= 1) return arr;
  
  const pivot = arr[0];
  const left = [];
  const right = [];

  for (let i = 1; i < arr.length; i++) {
    if (arr[i] < pivot) {
      left.push(arr[i]);
    } else {
      right.push(arr[i]);
    }
  }

  return quickSort(left).concat(pivot, quickSort(right));
}

const arr = [4, 8, 2, 1, 3, 5, 9];
console.log(quickSort(arr)); // [1, 2, 3, 4, 5, 8, 9]
```
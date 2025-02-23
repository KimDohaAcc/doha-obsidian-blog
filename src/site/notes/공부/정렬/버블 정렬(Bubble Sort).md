---
{"dg-publish":true,"permalink":"/공부/정렬/버블 정렬(Bubble Sort)/","dgPassFrontmatter":true}
---


![bubblesort.gif](/img/user/%EC%B2%A8%EB%B6%80%ED%8C%8C%EC%9D%BC/bubblesort.gif)

첫 번째 원소부터 인접한 원소와 비교하며 **자리를 바꾸면서** ==맨 끝부터== 정렬하는 방식

i번째 원소와 i+1번째 원소의 값을 비교하고,
만약 i번째 값이 i+1번째 값보다 크다면
둘의 자리를 바꾸어 *값이 큰 원소가 뒤에 위치*하게 한다

#### 시간복잡도
*(n-1) + (n-2) + ... + 2 + 1 = n(n-1)/2* 이므로 **O(n^2)**
어떤 경우에도 2개 원소를 비교하기 때문에 최선, 평균, 최악 모두 동일한 시간복잡도를 가진다

#### 특징
- 구현이 간단하고 직관적이다
- 정렬하고자 하는 배열 안에서 교환하므로  [[공부/정렬/제자리 정렬(Inplace algorithm)\|제자리 정렬(Inplace algorithm)]]이다
- [[공부/정렬/안정 정렬(Stable Sort)\|안정 정렬(Stable Sort)]]이다

#### 단점
시간복잡도가 O(n^2)
정렬된 상태에서 새로운 데이터가 추가될 때 정렬 효율이 좋지 않다

##### 개선된 양방향 버블 정렬
[[공부/정렬/칵테일 셰이커 정렬(Cocktail Shaker Sort)\|칵테일 셰이커 정렬(Cocktail Shaker Sort)]]이라고도 부른다

## 코드
```javascript
function bubbleSort(arr) {
  for (let i = 0; i < arr.length - 1; i++) {
    for (let j = 0; j < arr.length - i; j++) {
      if (arr[j] > arr[j + 1]) {
        const swap = arr[j];
        arr[j] = arr[j + 1];
        arr[j + 1] = swap;
      }
    }
  }
  return arr;
}

const arr = [4, 3, 8, 5, 2, 1];
console.log(bubbleSort(arr)); // [1, 2, 3, 4, 5, 8]
```
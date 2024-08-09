---
{"dg-publish":true,"permalink":"/공부/정렬/버킷 정렬(Bucket Sort)/","dgPassFrontmatter":true}
---

![Pasted image 20240809171842.png](/img/user/%EC%B2%A8%EB%B6%80%ED%8C%8C%EC%9D%BC/Pasted%20image%2020240809171842.png)

정렬되지 않은 자료를 *버킷*이라는 단위 기억 장소에 여러 그룹으로 정렬하고,
버킷 안의 요소들을 개별적으로 정렬한 후 다시 합치는 정렬 방식

#### 작동
1) 입력 데이터를 ==일정 범위==에 따라 여러 버킷에 분배한다
2) 버킷 안의 데이터를 ==개별적으로 정렬==한다
3) 각 버킷을 순서대로 합쳐 최종 결과를 생성한다

#### 특징
- 데이터가 균일하게 분포되어 있을 때 효율적이다
- 데이터가 특정한 값에 몰려 일부 버킷에 데이터가 많다면 성능이 저하된다
- [[공부/정렬/안정 정렬(Stable Sort)\|안정 정렬(Stable Sort)]]이다

#### 응용 분야
- 수치 데이터나 범주화된 데이터를 정렬하는 데 유용하기 때문에
  주로 그래픽스 처리, 데이터베이스의 키값 정렬, 데이터 분석 및 통계적 계산 등의 분야에서 활용된다

## 코드
```jsx
function bucketSort(arr, bucketSize = 5) {
  if (arr.length === 0) {
    return arr;
  }

  // Determine minimum and maximum values
  let minValue = arr[0];
  let maxValue = arr[0];
  for (let i = 1; i < arr.length; i++) {
    if (arr[i] < minValue) {
      minValue = arr[i];
    } else if (arr[i] > maxValue) {
      maxValue = arr[i];
    }
  }

  // Determine number of buckets
  const bucketCount = Math.floor((maxValue - minValue) / bucketSize) + 1;
  const buckets = new Array(bucketCount);
  for (let i = 0; i < buckets.length; i++) {
    buckets[i] = [];
  }

  // Distribute elements into buckets
  for (let i = 0; i < arr.length; i++) {
    const bucketIndex = Math.floor((arr[i] - minValue) / bucketSize);
    buckets[bucketIndex].push(arr[i]);
  }

  // Sort each bucket using insertion sort
  for (let i = 0; i < buckets.length; i++) {
    insertionSort(buckets[i]);
  }

  // Concatenate sorted buckets
  return buckets.reduce((acc, curr) => acc.concat(curr), []);
}

function insertionSort(arr) {
  for (let i = 1; i < arr.length; i++) {
    const current = arr[i];
    let j = i - 1;
    while (j >= 0 && arr[j] > current) {
      arr[j + 1] = arr[j];
      j--;
    }
    arr[j + 1] = current;
  }
}
```
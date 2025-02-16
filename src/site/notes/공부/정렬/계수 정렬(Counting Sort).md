---
dg-publish: true
---
![Pasted image 20240809153333.png](/img/user/%EC%B2%A8%EB%B6%80%ED%8C%8C%EC%9D%BC/Pasted%20image%2020240809153333.png)

요소 값들끼리 서로 ==비교하지 않고== 정렬하는 알고리즘

#### 시간복잡도
**O(N + K)** 으로 정렬 알고리즘 중 가장 빠르다
여기서 K는 배열의 최댓값이다

#### 공간복잡도
==O(배열 내 최댓값 + 1)== 길이 만큼의 배열이 필요하기 때문에 메모리가 낭비될 수 있다

#### 구현
1. 원소 값의 개수를 저장하는 ==카운팅 배열==을 만든다
2. 직전 요소들의 값을 더한 누적 배열로 만든다
![Pasted image 20240809153823.png](/img/user/%EC%B2%A8%EB%B6%80%ED%8C%8C%EC%9D%BC/Pasted%20image%2020240809153823.png)

1. 입력 배열과 동일한 크기의 출력 배열을 만들고, 입력 배열의 역순으로 출력 배열 요소를 채운다
![Pasted image 20240809154135.png](/img/user/%EC%B2%A8%EB%B6%80%ED%8C%8C%EC%9D%BC/Pasted%20image%2020240809154135.png)

#### 특징
- 데이터가 양수이고, 값의 범위가 너무 크지 않아야 한다 -> 배열의 인덱스를 이용하기 때문
- 그래서 정렬하는 숫자가 ==특정한 범위== 내에 있을 때 유용하다
- 정렬 알고리즘 중 ==가장 빠르다==
- 맨 뒤에서부터 값을 채우게 되면 [[공부/정렬/안정 정렬(Stable Sort)\|안정 정렬(Stable Sort)]]이다
- 만약 Unstable해도 상관 없다면 앞에서부터 채워도 된다
- 입력 데이터의 ==최댓값에 따라 메모리 낭비==가 심해질 수있다
- 제자리 정렬이 아니다

## 코드
```js
function countingSort(arr) {
  // 배열의 사이즈를 최대값 9가 담기도록 크게 잡기
  const MAX_DATA_VALUE = 10;
  const counting = new Array(MAX_DATA_VALUE).fill(0);

  for (let i = 0; i < arr.length; i++) {
    counting[arr[i]]++;
  }

  for (let i = 1; i < MAX_DATA_VALUE; i++) {
    counting[i] += counting[i - 1];
  }

  const sorted = new Array(arr.length).fill(0);

  for (let i = arr.length - 1; i >= 0; i--) {
    sorted[counting[arr[i]] - 1] = arr[i];
    counting[arr[i]]--;
  }

  return sorted;
}
```
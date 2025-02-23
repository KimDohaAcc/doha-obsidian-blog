---
{"dg-publish":true,"permalink":"///radix-sort/","dgPassFrontmatter":true}
---


---
dg-publish: true
---
![Pasted image 20240809160158.png](/img/user/%EC%B2%A8%EB%B6%80%ED%8C%8C%EC%9D%BC/Pasted%20image%2020240809160158.png)

*자릿수*를 기준으로 정렬하는 알고리즘

값들 간에 ==비교 연산을 하지 않고==,  정렬할 수 있다
Radix sort는 [[공부/정렬/LSD(Least Significant Digit)\|LSD(Least Significant Digit)]] Sort 방식이다

각 자리에서 [[공부/정렬/버킷 정렬(Bucket Sort)\|버킷 정렬(Bucket Sort)]]이나 [[공부/정렬/계수 정렬(Counting Sort)\|계수 정렬(Counting Sort)]]을 사용한다

#### 시간복잡도
**O(dN)** 이며, d는 데이터들의 최대 자릿수를 의미한다

#### 공간복잡도
기수 정렬은 각 자리수에 해당하는 값을 정렬하기 위해 *버킷*이나 *카운트 배열*을 생성하기 위해 메모리를 소모가 필수적이다.
이 메모리는 입력 데이터의 최댓값이나 자릿수의 범위 크기에 따라 결정된다. 

#### 메모리 사용 최적화
###### 병렬 처리 기술
최근 기수 정렬 최적화에서는 병렬 처리 기술이 널리 사용된다. 각 자릿수에 대해 동시에 정렬 작업을 수행한다.

#### 특징
- 문자열, 정수 정렬이 가능하다
  -> 음수가 있을 경우 음수를 따로 빼내서 똑같은 방법으로 정렬한 후, 결과를 양수와 합치는 식으로 할 수 있다
  - [[공부/정렬/안정 정렬(Stable Sort)\|안정 정렬(Stable Sort)]]이다
  - 자릿수가 없는 것은 정렬할 수 없다(ex. 부동소수점)
  - 중간 결과를 저장할 bucket의 공간이 필요하다
  - 제자리 정렬이 아니다

#### 사용처
데이터베이스 작업, 인덱스 생성, 정렬 병합 조인과 같은 ==데이터 집합 정렬 핵심 작업==에 활용된다.
대량의 데이터를 처리하는 상황에서 효율성이 높다.

## 코드
```js
function getMaxDigit(arr) {
  let maxDigit = 0;
  for (let i = 0; i < arr.length; i++) {
    maxDigit = Math.max(maxDigit, `${arr[i]}`.length);
  }
  return maxDigit;
}

function radixSort(arr) {
  const maxDigit = getMaxDigit(arr);

  for (let x = 0; x < maxDigit; x++) {
    let digitBucket = new Array(10).fill(0).map((_) => []);
    for (let i = 0; i < arr.length; i++) {
      let digit = Math.floor(Math.abs(arr[i]) / Math.pow(10, x)) % 10;
      digitBucket[digit].push(arr[i]);
    }
    arr = [].concat(...digitBucket);
  }

  return arr;
}
```
---
{"dg-publish":true,"permalink":"/공부/정렬/LSD(Least Significant Digit)/","dgPassFrontmatter":true}
---

낮은 자릿수부터 정렬을 진행해 나가는 방식

주로 반복문으로 구현된다.
각 자릿수마다 안정적인 정렬 알고리즘을 적용한다.

#### 특징
- 구현이 간단하다
- 정렬이 끝날 때까지 정렬 결과를 파악할 수 없다
- 자릿수가 정해진 경우, 좀 더 빠를 수 있다
- [[공부/정렬/안정 정렬(Stable Sort)\|안정 정렬(Stable Sort)]] 방식이다
- 입력 데이터 분포에 관계없이 일정한 성능을 낸다
- 각 자릿수별로 독립적으로 처리할 수 있어 병렬화하기 쉽다
- 대규모 데이터셋에서 LSD가 더 효율적이고 안정적이다

반대되는 개념으로 [[공부/정렬/MSD(Most Significant Digit)\|MSD(Most Significant Digit)]]가 있다

## 코드
```python
def lsd_radix_sort(arr):
    max_num = max(arr)
    exp = 1
    n = len(arr)
    
    while max_num // exp > 0:
        counting_sort(arr, exp)
        exp *= 10

def counting_sort(arr, exp):
    n = len(arr)
    output = [0] * n
    count = [0] * 10

    for i in range(n):
        index = arr[i] // exp
        count[index % 10] += 1

    for i in range(1, 10):
        count[i] += count[i - 1]

    i = n - 1
    while i >= 0:
        index = arr[i] // exp
        output[count[index % 10] - 1] = arr[i]
        count[index % 10] -= 1
        i -= 1

    for i in range(n):
        arr[i] = output[i]

# 사용 예
arr = [170, 45, 75, 90, 802, 24, 2, 66]
lsd_radix_sort(arr)
print("LSD 정렬 결과:", arr)
```
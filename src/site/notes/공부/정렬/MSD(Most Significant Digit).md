---
dg-publish: true
---
높은 자릿수부터 정렬을 진행해 나가는 방식

주로 재귀적으로 구현된다.

#### 특징
- 데이터의 ==자릿수가 많고==, ==범위가 넓은 경우==에 유리하다.
- 특히 ==문자열 정렬==이나 ==특정 패턴==을 가진 데이터의 경우에 적합하다.
- 끝까지 가지 않아도 중간에 정렬이 완료될 수 있다는 것이 장점이다
- 그러나 이를 위해서는 중간 점검을 해야한다
- 중간 점검 때문에 [[공부/정렬/LSD(Least Significant Digit)\|LSD(Least Significant Digit)]]에 비해 구현이 복잡하다
- 재귀적으로 구현될 때 추가 메모리 공간이 필요하다
- 데이터 분포에 따라 성능 차이가 클 수 있다
## 코드
```python
def msd_radix_sort(arr):
    max_num = max(arr)
    max_digits = len(str(max_num))
    return msd_radix_sort_helper(arr, max_digits, 0, len(arr) - 1)

def msd_radix_sort_helper(arr, d, low, high):
    if low >= high or d == 0:
        return arr
    
    buckets = [[] for _ in range(10)]
    divisor = 10 ** (d - 1)
    
    for i in range(low, high + 1):
        digit = (arr[i] // divisor) % 10
        buckets[digit].append(arr[i])
    
    index = low
    for bucket in buckets:
        if len(bucket) > 1:
            msd_radix_sort_helper(bucket, d - 1, 0, len(bucket) - 1)
        for num in bucket:
            arr[index] = num
            index += 1
    
    return arr

# 사용 예
arr = [170, 45, 75, 90, 802, 24, 2, 66]
msd_radix_sort(arr)
print("MSD 정렬 결과:", arr)
```
---
{"dg-publish":true,"permalink":"/공부/알고리즘/좌표 압축(Coordinate Compression)/","dgPassFrontmatter":true}
---


수의 값과 상관 없이 **대소 관계**만 알면 될 때 이용하는 알고리즘

[[공부/자료구조/맵/HashMap\|HashMap]]이나  [[공부/알고리즘/탐색/이분 탐색(Binary Search)\|이분 탐색(Binary Search)]]을 사용한다

수의 범위가 크다면, 메모리를 절약하며 대소 관계를 파악할 수 있다

#### 진행 과정
1. 배열을 입력 받는다
2. 중복 제거 후 정렬된 배열을 만든다
3. 원본 좌표값들을 순회하면서 정렬된 배열에서 인덱스를 찾아 매핑한다

#### 코드

###### 해시맵
```python
def coordinate_compression(coords):
    # 1. 중복 제거 및 정렬
    sorted_coords = sorted(set(coords))
    
    # 2. 매핑 테이블 생성
    coord_map = {val: idx for idx, val in enumerate(sorted_coords)}
    
    # 3. 압축된 좌표로 변환
    compressed = [coord_map[x] for x in coords]
    
    return compressed

# 예시
original = [1000000, 2, 3, 2, 1000000]
compressed = coordinate_compression(original)
# 결과: [2, 0, 1, 0, 2]
```

###### 이분탐색
시간 복잡도는 O(NlogN) 정렬 + O(NlogM) 이분탐색
이분 탐색을 사용하면 추가 메모리 사용을 줄일 수 있다
```python
def coordinate_compression(coords):
    # 1. 중복 제거 및 정렬
    sorted_coords = sorted(set(coords))
    
    # 2. 이분 탐색으로 압축된 좌표 찾기
    def binary_search(arr, target):
        left, right = 0, len(arr) - 1
        while left <= right:
            mid = (left + right) // 2
            if arr[mid] == target:
                return mid
            elif arr[mid] < target:
                left = mid + 1
            else:
                right = mid - 1
        return -1
    
    # 3. 각 좌표값을 압축된 값으로 변환
    compressed = [binary_search(sorted_coords, x) for x in coords]
    
    return compressed
```

####  활용 사례

세그먼트 트리나 펜윅 트리 같은 자료구조
좌표 평면상 점들을 다룰 때
대소 관계 비교가 필요할 때
값의 범위가 매우 큰 정렬 문제를 해결할 때

#### 시간 복잡도
O(NlogN)
---
{"dg-publish":true,"permalink":"////two-pointers/","dgPassFrontmatter":true}
---


![two_pointer_image.png](/img/user/첨부파일/two_pointer_image.png)

**1차원 배열**에서 각자 다른 원소를 가리키고 있는 **2개의 포인터**를 원하는 값을 찾을 때까지 탐색하는 알고리즘

#### 동작 방식 및 구현
일반적으로 left, right 또는 start, end로 포인터에 이름을 붙이고 **배열의 양 끝 또는 같은 인덱스에 배치**한다

### 배열의 양 끝에 포인터를 두는 경우
left < right
target 보다 합이 작다면 : left ++
target 보다 합이 크다면 : right --

###### 적합한 문제
1. 배열의 **두 수의 합이 특정한 값**이 되는 원소 인덱스 찾기
2. 특정 값보다 작거나 같은 요소의 **최대 길이** 찾기

### 배열의 같은 인텍스에 포인터를 두는 경우
start == end == 0
target 보다 합이 작다면 : end ++
target 보다 합이 크다면 : start ++

###### 적합한 문제
1. 배열의 **연속 수열의 합**(i부터 j까지)이 특정한 값이 되는 시작점, 끝점 찾기
2. 특정 패턴이 나타나는 **최소 길이의 부분 문자열** 찾기
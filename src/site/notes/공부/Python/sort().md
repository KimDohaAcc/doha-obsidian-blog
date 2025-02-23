---
{"dg-publish":true,"permalink":"/공부/Python/sort()/","dgPassFrontmatter":true}
---


리스트 내장 함수로, 내부 원소를 정렬한다
sort()는 [[공부/Python/sorted()\|sorted()]]와 정렬 방식이 같으며, [[공부/정렬/병합 정렬(Merge sort)\|병합 정렬(Merge sort)]]과 [[공부/정렬/삽입 정렬(Insertion Sort)\|삽입 정렬(Insertion Sort)]]의 아이디어를 더한 하이브리드 방식의 정렬 알고리즘을 사용한다

#### 시간복잡도
병합 정렬은 [[공부/정렬/퀵 정렬(Quick Sort)\|퀵 정렬(Quick Sort)]]보다 느리지만, 최악의 경우에도 O(NlogN)을 보장하는 특징이 있다.
따라서 정렬 라이브러리의 시간 복잡도는 최악의 경우에도 ==O(NlogN)==이다

>[!note] sort의 프로토타입
>`<list>.sort(key = <function> , reverse = <bool>)`

#### reverse=True
reverse를 True로 주면 내림차순 정렬을 할 수 있다.
default 값은 False이다

#### key
[[공부/Python/sorted()\|sorted()]]나 sort()를 사용할 때 매개변수로 key를 받을 수 있다
key는 함수를 받기 때문에, 직접 반환 함수를 만들어서 넣어줘도 된다

##### 길이에 따라 정렬할 때
```python
my_list = ["api", "app", "carrier", "demon", "aaa"]
sorted_list = sorted(my_list, key=len)
```
key=len 으로 주면 길이가 짧은 순으로 오름차순 정렬이 된다

##### lambda 활용
```python
my_list = ["api", "app", "carrier", "demon", "aaa"]
sorted_list = sorted(my_list, key=lambda x : (len(x), x))
```
[[공부/Python/lambda\|lambda]] 함수를 사용하면 위와 같이 1순위 : 길이, 2순위 : 사전순으로 정렬할 수 있다
이렇게 2개의 정렬 조건이 필요한 경우 lambda를 쓰면 유용하다

##### 이중 리스트 정렬
```python
array = [[50, "apple"], [30, "banana"] , [400, "melon"\|50, "apple"], [30, "banana"] , [400, "melon"]]
array.sort(key=lambda x : x[0])
arrays.rot(key=lambda x : (x[0], -x[1]))
```
lambda 함수를 사용해서 이중 리스트를 정렬하는 것도 가능하다
튜플의 앞 쪽에 있는 기준이 더  순위가 높은 기준이 된다
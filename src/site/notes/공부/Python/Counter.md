---
{"dg-publish":true,"permalink":"/공부/Python/Counter/","dgPassFrontmatter":true}
---


collectrions 모듈의 Counter 클래스는 개수를 세는 ==계수기 도구==이다
자료구조는 아니다

Counter는 딕셔너리 형태로 key = 값, value = 개수 를 갖는다

리스트에서 사용할 수도 있고, 문자열에서 사용할 수도 있다
Counter끼리의 연산도 가능하다
###### 예시
```python
from collections import Counter

a = [1, 2, 5, 1, 5, 5, 5]
print(Counter(a)) # Counter({5:4, 1:2, 2:1})

b = 'aaabbbccdddd'
print(Counter(b)) 

c = 'abcd'
print(Counter(b) - Counter(c)) # Counter({'a':2, 'b':2, 'c':1, 'd':3})
```

###### 시간복잡도
하나의 리스트 또는 문자열을 순회하면서 Counter 객체를 생성하기 때문에 시간복잡도는 *O(N)* 이다
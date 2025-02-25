---
{"dg-publish":true,"permalink":"/공부/Python/lambda/","dgPassFrontmatter":true}
---


익명 함수(anonymous function)이라고도 부른다
말 그대로 이름이 없는 함수로, 일반적으로 함수를 한 번만 사용하거나 인자로 전달해야 하는 경우 유용하게 사용된다

#### 사용
```python
lambda 인자 : 표현식
```

람다 함수는 `def`를 사용해서 함수를 정의하는 것보다 간편한 방식으로 정의할 수 있다

```python
def add(x, y):  # def 함수
	return x + y

add_1 = add(x, y)
add_2 = lambda x, y : x + y  # lambda 함수

```
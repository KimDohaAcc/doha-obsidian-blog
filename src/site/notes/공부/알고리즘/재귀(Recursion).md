---
{"dg-publish":true,"permalink":"/공부/알고리즘/재귀(Recursion)/","dgPassFrontmatter":true}
---

자기 자신을 호출하여 순환 수행되는 것

여러가지 분기가 있을 때 사용하기 좋다


>[!example]
> - Base case : 기저 조건
>- Recursive case : 재귀 조건

모든 재귀함수는 반복문(iteration)으로 변경 가능하며
그 역도 성립한다. 즉, 모든 반복문은 recursion으로 표현 가능하다
재귀함수의 장점은 복잡한 알고리즘을 **단순하고 알기 쉽게 표현하는 것이 가능하다는 점!**

##### 문제점

간단한 문제에 대해서는 반복문에 비해 메모리 및 속도에서 성능 저하가 발생한다
피보나치 등을 구현할 때 수많은 중복 호출이 존재한다
👉 [[공부/알고리즘/DP(Dynamic Programming)\|DP(Dynamic Programming)]] 으로 개선할 수 있다
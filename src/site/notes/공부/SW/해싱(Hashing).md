---
{"dg-publish":true,"permalink":"/공부/SW/해싱(Hashing)/","dgPassFrontmatter":true}
---

![Pasted image 20240302181110.png](/img/user/%EC%B2%A8%EB%B6%80%ED%8C%8C%EC%9D%BC/Pasted%20image%2020240302181110.png)

해시 함수에 ==문자열 입력값을 넣어서 특정한 값으로 추출==하는 것을 의미

해싱은 키에 산술적인 연산을 적용하여 항목이 저장되어 있는 ==테이블의 주소를 계산==하여 항목에 접근한다

```
A -> 해시 함수 -> Alpha
B -> 해시 함수 -> Bravo
C -> 해시 함수 -> Cycle
```

위 예시에서 A는 [[공부/SW/해시 함수\|해시 함수]]가 바뀌지 않는 한 해싱 헀을 때 Alpha라는 일정한 값이 나온다
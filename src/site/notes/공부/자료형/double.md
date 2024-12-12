---
{"dg-publish":true,"permalink":"/공부/자료형/double/","dgPassFrontmatter":true}
---

실수를 표현하기 위해 사용하는 자료형
double precision이라고도 한다

[[공부/자료형/float\|float]]가 4Byte인 것에 비해 double은 **8Byte=64bit**이다
둘의 차이는 ==정밀도==에 있다고 할 수 있다

표현할 수 있는 데이터의 범위는 -1.7 x 10^308 ~ 1.7 x 10^308 이다

##### 구성
부호(1bit) + 지수 부분(11bit) + 유효숫자 부분(52bit) = 64bit
![Pasted image 20240730142725.png](/img/user/%EC%B2%A8%EB%B6%80%ED%8C%8C%EC%9D%BC/Pasted%20image%2020240730142725.png)
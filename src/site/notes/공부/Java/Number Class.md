---
{"dg-publish":true,"permalink":"/공부/Java/Number Class/","dgPassFrontmatter":true}
---

숫자를 멤버변수로 갖는 클래스의 조상 클래스

![Pasted image 20240821133337.jpg](/img/user/%EC%B2%A8%EB%B6%80%ED%8C%8C%EC%9D%BC/Pasted%20image%2020240821133337.jpg)


[[공부/Java/변수(variable)/변수의 타입\|변수의 타입]] 중 숫자형 primitive type에 대응되는 [[공부/Java/Wrapper Class\|Wrapper Class]]들은 모두 Number 클래스의 자손이다.

즉, Byte, Short, Integer, Long, Float, Double은 Number 클래스의 자손이다.
덧붙여 BigInteger와 BigDecimal도 Number의 자손이다

###### BigInteger

long으로도 다룰 수 없는 큰 범위의 정수를 처리하는 클래스

###### BigDecimal

double로도 다룰 수 없는 큰 범위의 부동소수점 숫자를 처리하는 클래스
---
{"dg-publish":true,"permalink":"/공부/알고리즘/DP(Dynamic Programming)/","dgPassFrontmatter":true}
---


다이나믹 프로그래밍은 동적(Dynamic) 계획법이라고도 불린다
자료구조에서 동적 할당은 프로그램이 실행되는 ==도중에 실행에 필요한 메모리를 할당하는 기법==을 의미한다

큰 문제를 작은 문제로 나누어 푼다
➡ **한 번 계산한 문제는 다시 계산하지 않는다**

>[!tip] DP를 사용할 수 있는 조건
>1. [[공부/알고리즘/최적 부분 구조\|최적 부분 구조]]
>2. 중복되는 부분 문제
>	작은 문제를 동일하게 반복적으로 해결할 수 있다.

##### 메모이제이션(Memoization)
DP를 구현하는 방법 중 한 종류
한 번 구한 결과를 메모리 공간에 메모해두고, 메모한 결과를 가져와 사용한다.

##### 탑다운(Top-Down) vs 바텀업(Bottom-Up)
###### 탑다운
큰 문제를 해결하기 위해 작은 문제를 호출(==재귀==)하는 방식
탑다운(==메모이제이션==) 방식은 ==하향식==이라고도 한다

###### 바텀업
가장 작은 문제들부터 답을 구해가며 전체 문제의 답을 찾는 방식
바텀업 방식은 ==상향식==이라고도 한다
재귀 호출을 하지 않기 때문에 시간과 메모리 사용량을 줄일 수 있다는 장점이 있다

바텀업으로 피보나치 수열을 구현했을 때
```python
# 앞서 계산된 결과를 저장하기 위한 DP 테이블 초기화
dp = [0] * 100
dp[1] = 1
dp[2] = 1
n = 99

# 피보나치 수열 반복문으로 구현(Bottom-Up DP)
for i in range(3, n + 1):
    dp[i] = dp[i - 1] + dp[i - 2]

print(dp[n])
```

#### DP 유형 파악 방법
1. 그리디, 시뮬레이션, 완전탐색 등의 알고리즘으로 풀 수 없다고 생각이 들면 DP를 사용해보자
2. 일단 비효율적인 재귀로 프로그램을 작성한 뒤에, 메모이제이션을 적용할 수 있으면 코드를 개선하는 방법도 좋다
3. 최적화(최대, 최소값) 또는 경우의 수를 구할 때 사용한다
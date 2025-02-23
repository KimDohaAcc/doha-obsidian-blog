---
{"dg-publish":true,"permalink":"/공부/알고리즘 문제 풀이/BOJ_1149_RGB거리/","dgPassFrontmatter":true}
---


[[공부/알고리즘/DP(Dynamic Programming)\|DP(Dynamic Programming)]] 유형 중 ==최소비용 경로 문제==에 해당한다

집은 R, G, B 3가지 색으로 칠해질 수 있으며, 최소 비용으로 집을 칠해야 한다
단, 앞뒤로  같은 색을 칠할 수는 없다

문제를 차근차근 이해해보자

1) 1차원 배열로 처리할 수 있을까?

	만약 1차원 배열로 처리할 수 있다면, 색의 구분이 없는 배열이어야 한다.
	그렇다는 말은 i번째 자리에서 빨강, 초록, 파랑 중 *선택할 수 있는 기준*이 있으며, 최종적으로 n번째 집까지의 색칠 비용을 최소로 만들 수 있다는 것이다. 즉, 어떤 기준에 따라 부분 문제인 `dp[i]`도 i까지의 최소 색칠 비용을 보장해야 한다.
	
	그러나 생각해보면 i번째 자리에서 ==최소 비용을 보장해 줄 수 있는 선택은 없다==. 왜냐면 그리디하게 i번째에서 최소 색칠 비용을 고르더라도, 색이 겹치지 않아야 한다는 조건에 의해 ==다른 색을 선택했을 때 결과적으로 더 적은 비용==이 될 수 있기 때문이다.

	그래서 1차원 배열만으로는 불가능하다

2) 점화식은 어떻게 구성해야 할까?

	색깔에 의한 구분 기준을 넣어주는 것이 필요한 건 알겠고, 이제 dp배열을 정의해야 한다.
	n에 도달하기 위해 둘 중 한 칸은 진행 척도인 i가 들어가야 하며,
	색을 구분해야 하므로 color 를 결정하는 변수도 하나 있을 것이다.

	중요한 것은 어떤 색을 어떻게 칠할지 결정되는 바가 있냐는 것이다. 생각해보면 i번째 집의 색을 결정하면 i번째 집까지의 최소 비용을 구할 수 있다.

	`dp[red][3]`을 예로 들어보면, `dp[green][2]`와 `dp[blue][2]` 중 작은 값에 3번 집을 빨간색으로 칠하는 비용을 더한 것이 `dp[red][3]`의 최소 비용이 될 것이다.
	이로써 dp의 부분 최소 비용이 보장되며, 부분 문제의 합으로 `dp[color][n]`는 ==n번째 집을 color 로 칠했을 때의 최소 비용==이 된다.
	
	이를 일반화 하면 `dp[color][i] = min(dp[other_color1][i-1], dp[other_color2][i-1]) + painting[i][color]`
	이렇게 작성할 수 있다.

	그렇다면 궁극적인 최소 비용은 `dp[red][n], dp[green][n], dp[blue][n]`  중 가장 작은 비용이 될 것이다.
	
```python
import sys  
  
N = int(sys.stdin.readline())  
paint = [[0, 0, 0\|0, 0, 0]] + [list(map(int, sys.stdin.readline().split())) for _ in range(N)]  
MAXIMUM = 10000001  
RED = 0  
GREEN = 1  
BLUE = 2  
colors = [RED, GREEN, BLUE]  
# 빨강 초록 파랑  
# 비용의 최솟값  
# dp[][]  
  
dp = [[0] * (N + 1) for _ in range(3)]  
dp[RED][1] = paint[1][RED]  
dp[GREEN][1] = paint[1][GREEN]  
dp[BLUE][1] = paint[1][BLUE]  
  
for i in range(2, N + 1):  
    for color in colors:  
        color_1 = color + 1 if color + 1 < 3 else color - 2  
        color_2 = color + 2 if color + 2 < 3 else color - 1  
        dp[color][i] = min(dp[color_1][i - 1], dp[color_2][i - 1]) + paint[i][color]  
  
print(min(dp[RED][N], dp[GREEN][N], dp[BLUE][N]))
```
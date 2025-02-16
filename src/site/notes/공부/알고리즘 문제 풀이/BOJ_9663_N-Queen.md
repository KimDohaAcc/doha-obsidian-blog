---
dg-publish: true
---
[[공부/알고리즘/백트래킹\|백트래킹]]을 사용해서 N x N 체스판에 퀸 N개를 놓는 문제
2차원 배열로 풀면 경우의 수가 너무 많다
그림을 그려보면 1차원 배열로 풀 수 있다는 걸 느낄 수 있다

###### 가로, 세로, 대각선 침범 금지

퀸의 속성에 따라 서로 공격하지 않게 N개를 놓기 위해서는
마치 스도쿠처럼 **같은 행, 같은 열에 퀸이 겹치면 안 된다**
예를 들어 N=5라면 5개의 퀸은 각각 1, 2, 3, 4, 5로 서로 다른 행과 열을 가져야 한다

여기까지 구상하면 일차원 배열로 풀 수 있다는 걸 눈치챈다
dfs 함수를 이용해 각 행에 대해서
이제껏 방문하지 않은 열을 탐색하면 되기 때문이다
그러므로 ==visited는 열에 대해서만== 주면 된다

즉, 반복문을 돌면서
1) 방문한 열인지를 확인한다
2) 대각선 범위에 놓이는지 확인한다

대각선 범위라면 기울기는 *절댓값 1*을 가질 것이다
*abs(i-x) / abs(j-y) 가 1*이면 대각선 범위에 있는 위치이다

가로, 세로는 확인하지 않아도 된다
행은 한 번 뽑을 때마다 +1씩 늘어나서 안 겹치고
열은 visited로 안 겹치게 뽑기 때문이다

```python
N = int(input())  
count = 0  
  
  
def n_queen(n, queen_list, idx_x, visited_y):  
    if len(queen_list) == n:  
        global count  
        count += 1  
        return  
  
    for i in range(n):  
        if i in visited_y:  
            continue  
  
        # 아직 방문하지 않은 열  
        # 직전에 뽑은 queen들을 대각선으로 공격하지 않는지 비교  
        flag = False  
        for queen in queen_list:  
            if abs(idx_x - queen[0]) / abs(i - queen[1]) == 1:  
                flag = True  
                break  
        if not flag:  
            queen_list.append((idx_x, i))  
            n_queen(n, queen_list, idx_x + 1, visited_y + [i])  
            queen_list.pop()  
  
  
n_queen(N, [], 0, [])  
print(count)
```
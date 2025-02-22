---
{"dg-publish":true,"permalink":"/공부/알고리즘/그리디(Greedy) 알고리즘/","dgPassFrontmatter":true}
---


각 단계에서 국소적으로 최적인 선택을 하는 알고리즘

그리디 알고리즘은 대부분 국소 최적화가 전체 최적화를 이룬다는 것이 수학적으로 증명되어 있다

#### 예시

###### 활동 선택 문제

여러 활동의 시작 시간과 종료 시간이 주어졌을 때, 겹치지 않게 가장 많은 활동을 선택하는 문제
가장 일찍 끝나는 활동을 먼저 선택한다

###### 분할 가능한 배낭 문제

각 물건의 무게와 가치가 주어지고, 물건을 쪼갤 수 있을 때 배낭에 담을 수 있는 가장 가치 있는 조합을 찾는 문제
단위 무게 당 가치가 높은 물건부터 담는다

###### 허프만 코딩

문자의 빈도수에 따라 가변 길이 코드를 생성하여 데이터를 압축하는 알고리즘
가장 빈도가 낮은 두 문자/부분 트리를 반복적으로 결합

###### 최소 신장 트리

[[공부/알고리즘/크루스칼 알고리즘(Kruskal Algorithm)\|크루스칼 알고리즘(Kruskal Algorithm)]]과 [[공부/알고리즘/프림 알고리즘(Prim's Algorithm)\|프림 알고리즘(Prim's Algorithm)]] 모두 그리디 방식으로 최소 신장 트리를 찾는다

###### 동전 거스름돈 문제

거스름돈을 줄 때 사용하는 동전의 개수를 최소화하는 문제
가장 큰 단위의 동전부터 사용한다

###### 구간 스케줄링 문제

여러 작업의 시작 시간과 종료 시간이 주어졌을 때, 겹치지 않는 최대 개수의 작업을 선택하는 문제

가장 일찍 끝나는 작업부터 선택한다

###### 다익스트라 알고리즘
[[공부/알고리즘/다익스트라(Dijkstra) 알고리즘\|다익스트라(Dijkstra) 알고리즘]]에도 그리디가 사용된다
매 단계에서 가장 가까운 미방문 정점을 선택한다
---
dg-publish: true
---
정렬 알고리즘의 일종

###### 위상(Topology)

순서나 계층적인 구조를 의미, '앞뒤 순서 관계'

예를 들어 대학교 수강 과목의 선수강 과목 -> 후수강 과목이나
프로젝트의 기획 -> 개발 -> 테스트 같은 순서를 말한다

###### 위상정렬

사이클이 없는 방향 그래프인 [[공부/자료구조/트리/비순환 방향 그래프(DAG-Directed Acyclic Graph)\|비순환 방향 그래프(DAG-Directed Acyclic Graph)]]의 모든 노드를 *방향성을 지키며 순서대로 나열*하는 알고리즘

노드의 선행 관계를 고려하여 정점을 일렬로 나열하는 기법이다.
특정 작업이 완료되어야 다음 작업을 시작할 수 있는 경우에 사용된다.

###### 특징

**여러 위상 정렬 가능** : 하나의 방향 그래프에는 여러 가지 위상 정렬이 존재할 수 있디
**위상 순서** : 위상 정렬의 과정을 통해 선택된 정점의 순서를 위상 순서(Topological Order)라고 부른다
**중단 조건** : 위상 정렬 과정에서 진입 차수가 0인 정점이 남아있지 않다면 중단된다

###### 로직

1. 진입 차수가 0인 정점 선택
2. 큐에 삽입
3. 선택한 정점과 연결된 모든 간선 삭제
4. 선택한 정점에 속한 모든 간선에 대해 간선의 수를 감소
5. 반복

###### 활용 사례

학습 및 교육 과정 제시 - 특정 과목 수강 전, 선수 과목 이수가 필요할 때 올바른 수강 순서를 제시

작업 스케줄링 - 작업 수행 순서 결정

컴파일러 종속성 해결 - 먼저 컴파일 되어야 하는 파일의 순서 결정

버전 관리 시스템 - Git 과 같은 버전 관리 시스템에서 브랜치 생성, 병합 과정에 순서 결정

소프트웨어 배포 - 패키지 관리에서 각 패키지가 다른 패키지에 의존하고 있을 경우 올바른 순서로 설치하기 위해 위상 정렬 활용할 수 있음

==이처럼 다양한 작업에서의 선행 관계를 정리하고 효율적인 작업 관리할 때 유용==

#### 구현

In-degree를 사용하는 [[공부/알고리즘/탐색/너비 우선 탐색(BFS)\|너비 우선 탐색(BFS)]]나 [[공부/알고리즘/탐색/깊이 우선 탐색(DFS)\|깊이 우선 탐색(DFS)]]를 사용한다

##### 진입 차수 기반(BFS) 방법

각 정점의 진입 차수를 게산한 후, 진입 차수가 0인 정점을 큐에 추가하여 진행

###### 코드
```python
from collections import deque

def topological_sort(vertices, edges):
    # 그래프 초기화 및 진입 차수 배열
    graph = [[] for _ in range(vertices)]
    in_degree = [0] * vertices
    
    # 그래프 구성 및 진입 차수 계산
    for a, b in edges:
        graph[a].append(b)
        in_degree[b] += 1
        
    # 진입 차수가 0인 정점 큐에 추가
    queue = deque([i for i in range(vertices) if in_degree[i] == 0])
    result = []
    
    while queue:
        node = queue.popleft()
        result.append(node)
        
        for neighbor in graph[node]:
            in_degree[neighbor] -= 1
            if in_degree[neighbor] == 0:
                queue.append(neighbor)
                
    # 모든 정점이 방문되었는지 확인
    if len(result) == vertices:
        return result
    else:
        return None  # 사이클이 존재

# 예시: 5개의 정점과 6개의 간선 (0 -> 1, 0 -> 2, 1 -> 3, 1 -> 4, 2 -> 4, 3 -> 4)
vertices = 5
edges = [(0, 1), (0, 2), (1, 3), (1, 4), (2, 4), (3, 4)]
print(topological_sort(vertices, edges))
```

##### 깊이 우선 탐색(DFS) 방법

방문한 정점을 스택에 추가하는 방식

재귀를 통해 연결된 정점을 따라가다가 더 이상 방문할 노드가 없다면 `T[]`에 추가해주는 방식

![Pasted image 20241106102509.png](/img/user/%EC%B2%A8%EB%B6%80%ED%8C%8C%EC%9D%BC/Pasted%20image%2020241106102509.png)


```python
def topological_sort_dfs(vertices, edges):
    graph = [[] for _ in range(vertices)]
    for a, b in edges:
        graph[a].append(b)
    
    visited = [False] * vertices
    stack = []
    
    def dfs(node):
        visited[node] = True
        for neighbor in graph[node]:
            if not visited[neighbor]:
                dfs(neighbor)
        stack.append(node)
    
    for i in range(vertices):
        if not visited[i]:
            dfs(i)
    
    return stack[::-1]  # 역순으로 반환

# 예시: 5개의 정점과 6개의 간선
vertices = 5
edges = [(0, 1), (0, 2), (1, 3), (1, 4), (2, 4), (3, 4)]
print(topological_sort_dfs(vertices, edges))
```

###### 시간 복잡도

인접 리스트를 사용할 때 O(V+E)
인접 행렬을 사용할 때 O(V^2)
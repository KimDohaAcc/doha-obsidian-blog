---
{"dg-publish":true,"permalink":"/공부/알고리즘/다익스트라(Dijkstra) 알고리즘/","dgPassFrontmatter":true}
---

음의 가중치가 없는 그래프의 한 정점에서 모든 정점까지의 **최단 거리**를 각각 구하는 알고리즘(최단 경로 문제, Shortest Path Problem)으로 **그리디** 알고리즘에 속한다.

다익스트라는 변형이 많다. 원래 알고리즘은 **두 꼭짓점 간의 가장 짧은 경로를 찾는** 알고리즘이지만, 더 일반적인 변형은 한 꼭짓점을 **소스 꼭짓점**으로 고정하고 그래프의 다른 모든 꼭짓점까지의 최단 경로를 찾는 알고리즘으로 **최단 경로 트리**를 만드는 것이다.

모든 정점에서 다른 모든 정점은 아닌것에 주의, 이걸 원한다면 [[공부/알고리즘/플로이드 워셜 알고리즘(Floyd-Warshall Algorithm)\|플로이드 워셜 알고리즘(Floyd-Warshall Algorithm)]]을 써야한다

#### 알고리즘의 바탕이 되는 논리

> [!note] 
> *R이 P에서 Q로 가는 최단 경로에 있는 꼭짓점이라면, 이 경로는 마찬가지로 P에서 R까지 가는 최단 경로*라는 사실을 이용한다

벨먼의 유명한 최적성의 원리를 최단 경로 문제의 맥락에서 해석한 것이다.

#### 시간복잡도
**O((V+E)logV)**(V는 정점의 개수, E는 한 정점의 주변 노드)
➡ 각 노드마다 미방문 노드 중 출발점으로부터 현재까지 계산된 최단 거리를 가지는 ==노드를 찾는데== O(VlogV)의 시간이 필요하고 각 노드마다 ==이웃한 노드의 최단 거리를 갱신==할 때 O(ElogV)의 시간이 필요하기 때문이다

#### 그래프 방향
무향, 유향 상관 없으나 간선 중 하나라도 가중치가 음수면 사용할 수 없다.
음수인 경우 [[공부/알고리즘/벨만-포드 알고리즘(Bellman-Ford Algorithm)\|벨만-포드 알고리즘(Bellman-Ford Algorithm)]]을 사용 가능하다.

#### 실제 이용
큐브, 내비게이션(도시:노드, 도로:간선), 미로 탐색, 라우팅 OSPF

#### 구현
1. 출발점으로부터 **최단거리를 저장할 배열 d[v]** 를 만든다.
2. **출발 노드에는 0**을, 다른 노드에는 **INF**(최대값)를 채워넣는다.
3. **방문 배열을 생성**하여 방문했던 노드는 재방문하지 않게 한다.[[공부/알고리즘/다익스트라(Dijkstra) 알고리즘#^visited\|#^visited]]
4. 출발 노드의 번호를 **변수([[공부/SW/자료구조/Priority Queue\|Priority Queue]])** 에 저장한다.
5. 미방문 상태인 출발 노드에서 `d[A] + P[A][B]` 와 `d[B]`의 값을 비교한다.(P는 가중치 배열)
6. 전자가 짧다면 `d[B]` 의 값을 전자로 **갱신**시킨다.
7. A에 이웃한 모든 노드에 대해 작업을 수행한 후, A의 상태를 **방문 완료**로 바꾼다.
8. **미방문 상태**인 모든 노드들 중 출발점으로부터 거리가 가장 짧은 노드를 골라(Priority Queue를 썼다면 해당 과정이 필요 없다) **변수에 저장**한다.
9. 도착 노드가 방문 완료 상태가 되거나, 혹은 더 이상 미방문 상태의 노드가 없을 때까지 과정을 **반복**한다.
10. 작업을 마친 뒤 생성된 `d[x]`가 의미하는 바는 **시작점으로부터 노드 x까지의 최단 거리**이다.

```java
public class Dijkstra {
	static int V, E, start;
	static ArrayList<ArrayList<Node>> graph;

	static class Node {// 다음 노드의 인덱스와, 그 노드로 가는데 필요한 비용을 담고 있다.
		int idx, cost;

		Node(int idx, int cost) {
			this.idx = idx;
			this.cost = cost;
		}
	}

	public static void main(String[] args) throws IOException {
		// 초기화
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st = new StringTokenizer(br.readLine());
		V = Integer.parseInt(st.nextToken());
		E = Integer.parseInt(st.nextToken());
		start = Integer.parseInt(br.readLine());
		graph = new ArrayList<ArrayList<Node>>();
		for (int i = 0; i < V + 1; i++) {
			graph.add(new ArrayList<Node>());
		}
		for (int i = 0; i < E; i++) {
			st = new StringTokenizer(br.readLine());
			int s = Integer.parseInt(st.nextToken());
			int e = Integer.parseInt(st.nextToken());
			int c = Integer.parseInt(st.nextToken());
			// 문제에서는 유향 그래프에서의 다익스트라 알고리즘(이 조건도 문제에 따라 중요하다!).
			graph.get(s).add(new Node(e, c));
		}

		// 다익스트라 알고리즘 초기화
		int[] dist = new int[V + 1]; // 최소 비용을 저장할 배열
		for (int i = 0; i < V + 1; i++) {
			dist[i] = Integer.MAX_VALUE;
		}

		// 주의점 1. 다익스트라 알고리즘의 최소비용을 기준으로 추출해야 한다. 최대 비용을 기준으로 하는 경우 최악의 경우 지수시간 만큼의 연산을
		// 해야한다!
		PriorityQueue<Node> q = new PriorityQueue<Node>((o1, o2) -> Integer.compare(o1.cost, o2.cost));
		// 시작 노드에서, 시작 노드로 가는 값이 초기에 가장 짧은 비용을 갖는 노드이다.
		// 즉, 도착 정점은 start, 비용은 0인 노드를 가장 먼저 선택할 것이다.
		q.offer(new Node(start, 0));
		// 해당 노드를 선택한 것이나 마찬가지 이므로, dist[start] = 0으로 갱신.
		dist[start] = 0;
		while (!q.isEmpty()) {
			Node curNode = q.poll();

			// 목표 정점이 꺼내 졌다면, 해당 노드까지는 최솟값 갱신이 완료 되었다는 것이 확정이다(다익스트라 알고리즘).
			// 따라서, 반복문을 종료해도 되지만, 해당 코드는 시작 정점에 대하여 모든 정점으로의 최단 경로를 구하는 것을 가정한다.
			// 아래 주석된 코드는 목표 정점이 구해졌다면 빠르게 탈출할 수 있는 조건이다.
//			if (curNode.idx == end) {
//				System.out.println(dist[curNode.idx]);
//				return;
//			}

			// 꺼낸 노드 = 현재 최소 비용을 갖는 노드.
			// 즉, 해당 노드의 비용이 현재 dist배열에 기록된 내용보다 크다면 고려할 필요가 없으므로 스킵한다.
			// 주의점 2 : 중복노드 방지1 : 만일, 이 코드를 생략한다면, 언급한 내용대로 이미 방문한 정점을 '중복하여 방문'하게 된다.
			// 만일 그렇다면, 큐에 있는 모든 다음 노드에대하여 인접노드에 대한 탐색을 다시 진행하게 된다.
			// 그래프 입력이 만일 완전 그래프의 형태로 주어진다면, 이 조건을 생략한 것 만으로 시간 복잡도가 E^2에 수렴할 가능성이 생긴다.
			if (dist[curNode.idx] < curNode.cost) {
				continue;
			}

			// 선택된 노드의 모든 주변 노드를 고려한다.
			for (int i = 0; i < graph.get(curNode.idx).size(); i++) {
				Node nxtNode = graph.get(curNode.idx).get(i);
				// 만일, 주변 노드까지의 현재 dist값(비용)과 현재 선택된 노드로부터 주변 노드로 가는 비용을 비교하고, 더 작은 값을 선택한다.
				// 주의점 3 : 중복노드 방지 2 : 만일, 조건문 없이 조건문의 내용을 수행한다면 역시 중복 노드가 발생한다.
				// 간선에 연결된 노드를 모두 넣어준다면 앞서 언급한 정점의 시간 복잡도 VlogV를 보장할 수 없다.
				// 마찬가지로 E^2에 수렴할 가능성이 생긴다. 따라서 이 조건 안에서 로직을 진행해야만 한다.
				if (dist[nxtNode.idx] > curNode.cost + nxtNode.cost) {
					dist[nxtNode.idx] = curNode.cost + nxtNode.cost;
					// 갱신된 경우에만 큐에 넣는다.
					q.offer(new Node(nxtNode.idx, dist[nxtNode.idx]));
				}
			}
		}

		// 결과 출력
		System.out.println(Arrays.toString(dist));
	}
}
```
#### Priority Queue 구현 시 정렬
단순 Integer, int[] 로 구현
````java

// 1)
PriorityQueue<Integer> maxHeap = new PriorityQueue<(Collections.reverseOrder());

// 2)
PriorityQueue<Integer> queue = new PriorityQueue<>((o1, o2) -> {
	int abs1 = Math.abs(o1);
	int abs2 = Math.abs(o2);

	if(abs1 == abs2) return o1 > o2 ? 1 : -1;
	return abs1 - abs2;
});

````

class로 구현할 때는 Combarable을 implements 받아서 구현











### 각주

#### 방문처리{ #visited}


다시 탐색할 필요가 없기 떄문에 방문처리를 하여 똑같은 탐색을 하지 않게 한다.
1)  거리순으로 정렬을 해놓고 **거리가 짧은 순으로 방문**을 하는데,
2)  이는 그리디한 방식이지만 검증이 끝나서 **최솟값이 보장**되어 있다.
3)  따라서 한 번 방문했던 노드를 재방문할 필요가 없다!
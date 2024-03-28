---
{"dg-publish":true,"permalink":"/공부/알고리즘/크루스칼 알고리즘(Kruskal Algorithm)/","dgPassFrontmatter":true}
---

[[공부/SW/자료구조/트리/최소 스패닝 트리(MST)\|최소 스패닝 트리(MST)]] 를 구현하는 대표적인 알고리즘 중 하나

유니온 파인드를 활용하는 [[공부/알고리즘/서로소 집합\|서로소 집합]]의 좋은 사용 예이다

가중치가 가장 작은 간선일수록 최소 스패닝 트리에 포함된다는 발상으로 만들어졌다

**그리디**를 이용하여 ==네트워크의 모든 정점을 최소 비용으로 연결==하는 최적해답을 구하는 방법이다

그래프의 모든 간선을 오름차순으로 정렬한 뒤, 싸이클을 이루지 않게 트리에 더하는 방식으로 구현한다

#### 구현 과정
1. 그래프의 간선들을 가중치의 오름차순으로 정렬한다. 이를 위해 [[공부/SW/자료구조/Priority Queue\|Priority Queue]]를 활용한다.
2. 간선을 하나씩 확인하며 현재의 간선이 사이클을 발생시키는지 확인한다. 사이클을 형성하는 간선은 최소 신장 트리에서 제외한다.
3. 간선을 현재의 MST(최소 비용 신장 트리)의 집합에 추가한다.

#### 구현
```java
class Node implements Comparable<Node>{
	int to;
	int from;
	int value;
	
	public Node(int to, int from, int value) {
		this.to = to;
		this.from = from;
		this.value = value;
	}

	@Override
	public int compareTo(Node o) {
		return this.value - o.value;
	}
}

public class Main {
	private static int n; 	
	private static int[] parents;
	public static void main(String[] args) {
		n = 7; 
		int[][] graph = {{1,2,29}, {1,5,75},{2,3,35},{2,6,34}, {3,4,7},{4,6,23},
						{4,7,13}, {5,6,53}, {6,7,25}};
                        
		parents = new int[n + 1];
		for (int i=1; i<n+1; i++) { 
			parents[i] = i; 
		} 
        
		Queue<Node> pq = new PriorityQueue<>();
		for(int i=0; i<graph.length; i++) {
			int to = graph[i][0];
			int from = graph[i][1];
			int value = graph[i][2];
			// 우선순위 큐는 자동으로 간선 비용순(오름차순)으로 정렬된다.
			pq.add(new Node(to, from, value));			
		}
		
		int size = pq.size();
		int total =0;
		// 간선 하나씩 조회 (비용이 작은 간선부터)
		for(int i=0; i< size; i++) {
			 Node node = pq.poll();
			int rx = find(node.to);
			int ry = find(node.from);
			 
			 // 사이클이 발생하지 않는 경우에만 집합에 포함 
			 if(!isSameParent(rx, ry)) {
				 total += node.value;
				 union(node.to,node.from);
			 }
		}
		System.out.println(total);
	}
	
	static int find(int x) { 
		if (parents[x] == x) { 
			return x; 
	     } 
		return parents[x] = find(parents[x]);
	} 
	     
	static void union(int x, int y) {
		x = find(x); 
		y = find(y); 
		// 더 find 값으로 부모 노드 설정
	    if (x < y) { 
	    	parents[y] = x; 
	    } 
	    else { 
	    	parents[x] = y; 
	    } 
	}
	
	static boolean isSameParent(int x, int y) {
		if(rx == ry) return true;
		return false;
	} 
}
```
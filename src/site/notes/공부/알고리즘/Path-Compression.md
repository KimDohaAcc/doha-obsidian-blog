---
{"dg-publish":true,"permalink":"///path-compression/","dgPassFrontmatter":true}
---


---
{"dg-publish":true,"permalink":"/공부/알고리즘/Path-Compression/","dgPassFrontmatter":true}
---

[[공부/알고리즘/서로소 집합\|서로소 집합]] 최적화 방법 중 하나

Find-set을 행하는 과정에서 만나는 모든 노드들이  직접 root를 가리키도록 포인터를 바꾸어주는 방법

[[공부/알고리즘/Rank\|Rank]]와 함께 사용한다

````java
static int findset(int x) {
	// if(x == p[x]) return x;
	// return findset(p[x]);
	// path Compression 적용하면
	if(x != p[x]) p[x] = findset(p[x]);
	return p[x];
}
````
##### Path-Compression 주의점
대표자 변경이 되었음에도 불구하고 ==Fin-set이 일어난 노드==에 대해서만 경로 압축이 일어난다. 즉, 트리의 구조가 항상 대표를 직접 가리키고 있는 모양은 아니다.
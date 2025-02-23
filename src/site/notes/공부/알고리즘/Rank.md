---
{"dg-publish":true,"permalink":"///rank/","dgPassFrontmatter":true}
---


[[공부/알고리즘/서로소 집합\|서로소 집합]]의 최적화 방법 중 하나

노드의 subtree 높이를 rank로 저장

Union으로 집합을 합칠 때 rank가 낮은 집합을 높은 집합에 붙인다

rank가 같다면 둘 중 하나에 붙이고 랭크를 +1 해준다

#### Rank의 한계
[[공부/알고리즘/Path-Compression\|Path-Compression]]은 find-set을 할 때 일어나는 반면, Rank 갱신은 Union을 할 때 일어나기 때문에 경로 압축이 되어 높이가 변경됐음에도 불구하고 반영되지 않을  수 있다

-> 이를 완전히 해소하기 위해선 완전 탐색으로 모든 subtree를 탐색해야 하기에, 효율을 위해 rank는  ==보완== 용도로 생각하고 사용하는 것이 좋다
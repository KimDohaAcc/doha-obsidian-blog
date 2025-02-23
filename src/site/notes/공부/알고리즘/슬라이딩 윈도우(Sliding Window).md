---
{"dg-publish":true,"permalink":"///sliding-window/","dgPassFrontmatter":true}
---


윈도우, 즉 일정한 범위를 유지하면서 이를 이동시키는 알고리즘

예를 들어 2가지 긴 문자열이 주어지고, 알파벳을 **2개**만 포함하는 가장 긴 문자열을 찾는다면 슬라이딩 윈도우 알고리즘을 이용해서 풀 수 있다

>[!example]
> **AAAABBBBBBC**CCCCDDD
 AAAA**BBBBBBCCCCC**DDD

슬라이딩 알고리즘 활용은 대표적으로 Map을 이용하는 방법이 있다.
위와 같은 예시에서는 <알파벳, idx>로 각 위치를 기억해두면 빠르게 알파벳의 시작 위치를 기억할 수 있다

 >[!example]
 >map : [<"A", 0>, <"B", 5>, <"C", 11>, <"D", 16>]
 
 Map의 size가 3 이상이 되면 조건을 벗어나므로, 가장 작은 인덱스를 제거하고 새로운 인덱스를 Map에 넣으면 된다
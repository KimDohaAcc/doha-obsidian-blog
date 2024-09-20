---
{"dg-publish":true,"permalink":"/공부/알고리즘 문제 풀이/SQL/PGMS_잡은 물고기 중 가장 큰 물고기의 길이 구하기/","dgPassFrontmatter":true}
---

```MYSQL
select concat(max(length), 'cm') as max_length
from fish_info
```

CONCAT을 사용해서 뒤에 cm를 붙인다
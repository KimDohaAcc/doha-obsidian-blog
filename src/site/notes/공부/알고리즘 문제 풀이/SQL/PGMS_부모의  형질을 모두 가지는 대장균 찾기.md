---
{"dg-publish":true,"permalink":"///sql/pgms/","dgPassFrontmatter":true}
---


---
dg-publish: true
---
```mysql
SELECT
e.ID,
e.GENOTYPE,
p.GENOTYPE AS PARENT_GENOTYPE
FROM ECOLI_DATA e
JOIN ECOLI_DATA p
WHERE e.PARENT_ID = p.ID
AND e.GENOTYPE & p.GENOTYPE = p.GENOTYPE
ORDER BY ID
```

각 형질은 1, 5, 8 이런 식이고
부모의 형질은 이진수로 101, 자식 형질은 1101 이렇게 나올 수 있다
즉 자식은 부모의 1이 있는 이진수 자리를 항상 포함한다

모든 형질이 있는지를 파악하려면
101
1101
을 비트연산 했을 때
0101 이 나오게 되는데
이것이 부모의 형질과 같은지를 보면 된다
즉, 자식이 포함한 부모의 형질이 부모의 형질 자체와 같은지 확인한다
---
{"dg-publish":true,"permalink":"//database/sql/my-sql/case-when/","dgPassFrontmatter":true}
---


---
dg-publish: true
---
MySQL에서 CASE문은 프로그래밍 언어의 switch문과 비슷하다

### 사용법
```mysql
CASE
	WHEN 조건
	THEN '반환 값'
	WHERE 조건
	THEN '반환 값'
	ELSE '반환값'
END
```

### 예시
```mysql
SELECT
	idx,
    (CASE
		WHEN type = '1'
		THEN '의사'
		WHEN type = '2'
		THEN '장군'
		WHEN type = '3'
		THEN '왕'
		ELSE '일반인'
	END)
	AS hero_type,
	name
FROM hero_collection;
```
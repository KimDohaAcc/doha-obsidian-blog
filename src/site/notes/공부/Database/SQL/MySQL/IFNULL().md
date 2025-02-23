---
{"dg-publish":true,"permalink":"//database/sql/my-sql/ifnull/","dgPassFrontmatter":true}
---


---
dg-publish: true
---
해당 컬럼의 값이 NULL을 반환할 때, ==다른 값으로 출력할 수 있도록== 해주는 함수

### 사용법
```MYSQL
SELECT IFNULL(column명, "반환 값") FROM 테이블명;
```
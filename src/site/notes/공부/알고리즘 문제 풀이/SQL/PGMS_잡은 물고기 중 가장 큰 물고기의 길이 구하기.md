---
dg-publish: true
---
```MYSQL
select concat(max(length), 'cm') as max_length
from fish_info
```

CONCAT을 사용해서 뒤에 cm를 붙인다
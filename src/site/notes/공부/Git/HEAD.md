---
{"dg-publish":true,"permalink":"/공부/Git/HEAD/","dgPassFrontmatter":true}
---

현재 체크아웃된 ==브랜치를 가리키는 포인터==

즉, 현재 작업 중인 커밋을 가리키는 **참조(Reference)**

#### 주요 기능
- 현재 브랜치를 가리킨다.
- 체크아웃(checkout)한 특정 커밋을 가리킬 수도 있다.
- 새로운 커밋이 생성되면 HEAD가 자동으로 최신 커밋을 가리킨다.

#### HEAD 기본 구조
```
.git/
│── HEAD   # 현재 가리키는 브랜치 정보
│── refs/
│   ├── heads/
│   │   ├── main  # main 브랜치
│   │   ├── dev   # dev 브랜치

```
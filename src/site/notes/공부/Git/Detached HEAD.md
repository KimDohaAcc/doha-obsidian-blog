---
{"dg-publish":true,"permalink":"/공부/Git/Detached HEAD/","dgPassFrontmatter":true}
---

[[공부/Git/HEAD\|HEAD]]가 특정 브랜치가 아닌 특정 **커밋**을 직접 가리키는 상태

#### 진입
```bash
git checkout <커밋 해시>
```

이 상태에서 작업을 하면, ==브랜치 없이 커밋이 진행됨==
즉, Detached HEAD 상태에서 커밋을 하면 브랜치에 저장되지 않음

이후 커밋 시 ==새로운 커밋(커밋 해시 다름)==이 생성되지만, HEAD가 특정 브랜치와 연결되어 있지 않은 상태이므로, ==브랜치 히스토리와 연결되지 않음==

물론 Git 내부적으로는 해당 커밋을 보관하고 있음
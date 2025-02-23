---
{"dg-publish":true,"permalink":"/공부/Git/Packfile/","dgPassFrontmatter":true}
---


저장소의 데이터를 더 효율적으로 저장하고 전송하기 위한 ==압축된 데이터 파일==

[[공부/Git/Git의 4가지 내부 객체\|Git의 4가지 내부 객체]]를 하나의 **압축된 바이너리 파일**로 묶어 저장
#### 배경
일반적으로 [[공부/Git/Git\|Git]]은 개별 파일과 디렉토리를 `.git/objects/` 폴더에 해시값(SHA-1)을 기반으로 저장하는데, 프로젝트가 커지고 커밋이 많아질수록 저장해야 할 객체가 많아지고, 비효율적인 저장 방식이 됨

이를 최적화하기 위해 Packfile 도입

#### 구성 요소
- .pack 파일 : 여러 개의 Git 객체를 압축하여 하나의 파일로 저장
- .idx 파일 : Packfile 내 객체의 색인(index) 정보. 이를 통해 빠르게 검색 가능

#### Packfile 경로 예시
```
.git/
│── objects/
│   ├── pack/
│   │   ├── pack-abcdef123456.pack   # 압축된 Git 객체
│   │   ├── pack-abcdef123456.idx    # Packfile 색인 파일

```

#### 성능 향상
1. 저장 공간 절약 : 개별 객체보다 중복 제거 + 압축 적용. 같은 내용의 파일을 중복 저장하지 않고 재사용
2. 네트워크 전송 속도 향상 : git clone, git fetch, git pull, git push 시 Packfile이 사용되어 속도가 더 빠름
3. 빠른 객체 검색 : .idx 색인 파일이 Packfile 내부 객체를 빠르게 찾을 수 있도록 도움
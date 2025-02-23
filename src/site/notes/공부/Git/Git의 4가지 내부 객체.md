---
{"dg-publish":true,"permalink":"/공부/Git/Git의 4가지 내부 객체/","dgPassFrontmatter":true}
---


[[공부/Git/Git\|Git]]은 저장소 내 데이터를 관리하기 위해 4가지 객체(object)를 사용

1. 블롭(Blob, Binary Large Object) : 파일의 내용을 저장
2. 트리(Tree) : 폴더 구조를 저장
3. 커밋(Commit) : 특정 시점의 상태(Snapshot)을 저장
4. 태그(Tag) : 특정 커밋에 대한 고정된 마커

이 객체들은 [[공부/SW/해싱(Hashing)\|해싱(Hashing)]]된 SHA-1 해시값(40자리)를 기반으로 저장되며, `.git/objects/` 폴더 내에서 관리됨
---
{"dg-publish":true,"permalink":"///buffer/","dgPassFrontmatter":true}
---


---
{"dg-publish":true,"permalink":"/공부/SW/입출력/Buffer/","dgPassFrontmatter":true}
---

프로그래밍에서 Buffer는 CPU와 보조 기억 장치 사이에 사용되는 **임시 저장 공간**을 의미

데이터를 한 곳에서 다른 곳으로 전송하는 동안 일시적으로 그 데이터를 보관하는 메모리의 영역

자바에서는 데이터를 주고 받기 위해 [[공부/입출력/Stream\|공부/SW/입출력/Stream]]을 쓴다.
키보드, 마우스 등 입력 장치로부터 출력 장치로 내보낼 때 버퍼 안에 저장된다.
#### 버퍼링
버퍼를 활용하는 방식 또는 버퍼를 채우는 동작
순서대로 입출력 되어야 하므로 [[공부/자료구조/Queue\|Queue]]가 활용된다.

유튜브 회색 구간이 대표적!
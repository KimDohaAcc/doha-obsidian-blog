---
{"dg-publish":true,"permalink":"/공부/운영체제/정보(Information)/","dgPassFrontmatter":true}
---

Claude Shannon이 1930년대에 정보에 대해서 정의함

>[!info] 정보량 수식
>I(x) = -log<sub>2</sub> P(x)


어떤 사건 x가 있다면, 이 사건 x의 정보량(부피)은 ==이 사건이 발생할 확률==에 마이너스 로그를 붙인 것과 같다

###### 정보의 정의

정보란 불확실성을 측정해서 수치적으로 표현한 것

**정보의 최소 단위** : bit(binary digit)

###### 예시

주사위 = {1, 2, 3, 4, 5, 6}
-> 주사위를 굴려 3이 나왔다
-> A가 그 정보를 알고 있고, B는 모르는 상태
-> B가 주사위의 눈을 추측으로 맞출 수 있는 확률 : 1/6 = 6<sup>-1</sup>
-> -log<sub>2</sub>6<sup>-1</sup> = log<sub>2</sub>6

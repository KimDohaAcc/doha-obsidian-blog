---
{"dg-publish":true,"permalink":"/공부/JPA/Annotation/@EntityListeners/","dgPassFrontmatter":true}
---


이벤트를 관찰하고 있다가, 이벤트가 발생하면 특정 동작을 진행하는 것.

커스텀으로 class를 가져가도 되고,  AuditingEntityListener.class를 써도 된다

value값에 AuditingEntityListener.class를 넣어주고
Auditing에서 데이터가 생성될 때 업데이트 해주길 바라는 변수에 **@CreatedDate**를 붙인다
업데이트 해주길 바라는 변수에는 **@LastModifiedDate**를 붙인다

그 외
**@CreatedBy** : 생성한 사람 자동 저장
**@LastModifiedBy** : 수정한 사람 자동 저장

AuditingEntityListener를 사용하기 위해서는 Application 파일에 [[공부/JPA/Annotation/@EnableJpaAuditing\|@EnableJpaAuditing]]을 붙여줘야 한다
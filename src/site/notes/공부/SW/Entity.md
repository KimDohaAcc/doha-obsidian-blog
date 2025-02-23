---
{"dg-publish":true,"permalink":"//sw/entity/","dgPassFrontmatter":true}
---


Database의 테이블에 해당하며, 주로 하나의 테이블에 하나의 entity를 정의한다
테이블과 최대한 동일하게 클래스를 생성하고, 주로 테이블이 가지는 column들을 필드로 가진다

Entity를 다른 클래스, 메소드, 사용자와 직접 교환하는 것은 ==지양==한다
이러한 교환을 위해선 [[공부/SW/DTO(Data Transfer Object)\|DTO(Data Transfer Object)]]나 [[공부/SW/VO(Value Object)\|VO(Value Object)]]를 이용하는 것이 좋다
---
{"dg-publish":true,"permalink":"/공부/JPA/Annotation/@GeneratedValue/","dgPassFrontmatter":true}
---

기본키 자동 생성 어노테이션

##### @GeneratedValue(strategy = GenerationType.IDENTITY)
기본키 생성을 데이터베이스에게 위임하는 방식으로 id값을 따로 할당하지 않아도 데이터베이스가 자동으로 **AUTO_INCREMENT**를 하여 기본키를 생성해준다.

##### 그 외 
@GeneratedValue(strategy = GenerationType.SEQUNCE)
@GeneratedValue(strategy = GenerationType.TABLE)
@GeneratedValue(strategy = GenerationType.AUTO)

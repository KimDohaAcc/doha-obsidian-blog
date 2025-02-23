---
{"dg-publish":true,"permalink":"//spring//bean-scope/","dgPassFrontmatter":true}
---


#Bean

**Bean 정의를 작성하는 것은 Bean 객체를 생성하는 것과는 다르다!**

Bean 범위를 정의해서 객체의 범위를 제어할 수 있다 

[[공부/디자인 패턴/생성 패턴/Singleton\|Singleton]] : 기본값, Spring IoC 컨테이너에 대한 단일 객체 인스턴스

[[공부/디자인 패턴/생성 패턴/Prototype\|Prototype]] : 빈을 요청할 때마다 새로운 인스턴스 생성 

request : HTTP Request 주기로 bean 인스턴스 생성

session : HTTP Session 주기로 bean 인스턴스 생성
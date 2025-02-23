---
{"dg-publish":true,"permalink":"//spring//autowired/","dgPassFrontmatter":true}
---


---
{"dg-publish":true,"permalink":"/공부/Spring/스프링 기초/Autowired/","dgPassFrontmatter":true}
---

#Annotation

의존성 주입을 위한 [[공부/Spring/스프링 기초/Annotation\|Annotation]]

#### 사용 방법
의존성을 주입할 대상에 @Autowired annotation 작성 

Spring 컨테이너 내에서 타입 매칭 시행(컨테이너에 해당하는 타입의 bean이 있다면 매칭)

#### 사용 위치
생성자를 딱 하나만 정의한다면 → 사용 가능! 

만약 여러개다? Setter → @Qualifier를 이용하여 같은 타입이 여러 개일 경우, bean을 지정하여 식별 가능
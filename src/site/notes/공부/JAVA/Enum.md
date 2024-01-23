---
{"dg-publish":true,"permalink":"/공부/JAVA/Enum/","dgPassFrontmatter":true}
---

상수의 그룹을 나타낼 때 사용

#### 사용

````java
public enum Role { 
	USER, ADMIN; 
}
````

**[[공부/JPA/Annotation/@Enumerated\|@Enumerated]]** 어노테이션을 이용하면 EnumType을 사용할 수 있다
EnumType.ORDINAL 로 설정하면 순서가 저장되고 STRING으로 설정하면 Enum Type의 이름이 DB에 저장된다
````java
@Entity
@Getter
@Setter 
@NoArgsConstructor 
public Class User { 
@Id @Column @GeneratedValue(strategy = GenerationType.AUTO) 
private long id; 

@Column(name="user_name") 
private String userName; 

@Column 
private String password; 

@Enumerated(EnumType.STRING) 
private Role role; 
}
````
---
{"dg-publish":true,"permalink":"//jpa/annotation/enumerated/","dgPassFrontmatter":true}
---


Entity에서 속성으로 enum을 가질 때 쓰는 어노테이션

EnumType.ORDINAL 로 설정하면 순서가 저장되고 STRING으로 설정하면 Enum Type의 이름이 DB에 저장된다(ordinal 설정 후 enum 타입이 변경되면 순서가 변경되기 때문에 string 사용 권장)

#### 사용 예시

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
---
dg-publish: true
---
엔티티 객체의 데이터와 테이블의 컬럼과 매핑하는 관계를 **제외**하기 위해 사용하는 어노테이션

사용하면 ==해당 컬럼을 영속 대상에서 제외==시킨다
메소드, 필드에 선언할 수 있다

#### 사용
```java
@Entity
public class Member{
    @Id
    private Long id;
    private String userId;
    private String password;

    // [1] @Transient 선언
    javax.persistence.@Transient 
    private String confirmPassword; // 비밀번호 재입력 매핑 제외
}
```

비밀번호 재입력 필드처럼 굳이  테이블에 컬럼으로 구성해서 관리할 필요가 없다면 @Transient 어노테이션을 사용한다


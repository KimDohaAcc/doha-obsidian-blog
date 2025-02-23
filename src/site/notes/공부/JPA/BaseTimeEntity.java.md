---
{"dg-publish":true,"permalink":"//jpa/base-time-entity-java/","dgPassFrontmatter":true}
---


````java
@Getter 
@MappedSuperclass 
@EntityListeners(AuditingEntityListener.class) 
public abstract class BaseTimeEntity{ 
// Entity가 생성되어 저장될 때 시간이 자동 저장됩니다. 
@CreatedDate 
private LocalDateTime createdDate; 
// 조회한 Entity 값을 변경할 때 시간이 자동 저장됩니다. 
@LastModifiedDate 
private LocalDateTime modifiedDate; 
}
````

클래스를 상속 받으면 생성일자와 수정일자 컬럼을 인식해준다
#### @MappedSuperclass
JPA Entity 클래스들이 해당 추상 클래스를 상속할 경우 createDate, modifiedDate를 컬럼으로 인식

#### [[공부/JPA/Annotation/@EntityListeners\|@EntityListeners]](AuditingEntityListener.class)
해당 클래스에 Auditing 기능을 포함

#### @CreatedDate
Entity가 생성되어 저장될 때 시간이 자동 저장

#### @LastModifiedDate
조회한 Entity의 값을 변경할 때 시간이 자동 저장
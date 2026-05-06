---
{"dg-publish":true,"permalink":"/공부/ORM/JPA/Annotation/@SequenceGenerator/","dgPassFrontmatter":true,"dg-note-properties":{"permalink":"/공부/jpa/annotation/@sequencegenerator"}}
---


DB의 시퀀스를 기반으로 엔티티 PK 값을 자동 생성하는 어노테이션

name : 시퀀스 생성기의 이름을 지정
sequenceName : 시퀀스의 이름을 지정
allocationSize : 시퀀스 값의 할당 크기를 지정

````java
@Entity 
@SequenceGenerator(
name = "emp_id_generator", sequenceName = "emp_id_sequence", allocationSize = 1
) 
public class Employee {

  @Id 
  @GeneratedValue(strategy = GenerationType.SEQUENCE, generator = "emp_id_generator")
  private Long id; 
}
````
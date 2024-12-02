---
{"dg-publish":true,"permalink":"/공부/Java/ModelMapper/","dgPassFrontmatter":true}
---


서로 다른 클래스의 값을 한 번에 복사할 수 있게 도와주는 라이브러리

#### 장점
엔티티를 DTO로 복사하는 등 원하는 클래스에 넣어줄 때 실수가 발생하고 코드가 길어지는 문제를 해결해준다

#### 사용 
config를 추가해서 사용한다

````java
@Configuration 
public class ModelMapperConfig { 
	@Bean 
	public ModelMapper modelMapper(){ 
	return new ModelMapper(); 
	} 
}
````

````java
UserMapDto userMapDto = mapper.map(user, UserMapDto.class);
````

#### 스킵
````java
/**특정 필드 스킵*/ 
typeMap.addMappings(mapping -> {
	mapping.skip(Destination::setFieldName); 
}); 

/**null 필드 스킵*/ modelMapper.getConfiguration().setSkipNullEnabled(true); 

/*특정 null 필드 스킵*/ 
typeMap.addMappings(mapper -> mapper.when(ctx -> !ObjectUtils.isEmpty(ctx.getSource())) 
.map(UserDTO::getPassword, PersonDTO::setPassword));
````
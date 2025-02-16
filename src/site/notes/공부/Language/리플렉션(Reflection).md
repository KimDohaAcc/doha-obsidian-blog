---
dg-publish: true
---
실행 중인 프로그램이 자기 자신을 검사하고 수정할 수 있게 해주는 능력.
코드가 자기 자신을 들여다보고 조작할 수 있게 해주는 기능이다.

주로 [[공부/Java/자바(Java Programming Language)\|자바(Java Programming Language)]], C# 같은 객체 지향 프로그래밍 언어에서 많이  사용된다

###### 특징

1. 클래스의 메소드, 필드, 생성자 등의 정보를 실행 중에 알아낼 수 있다
2. 클래스의 객체를 동적으로 생성할 수 있다
3. 메소드를 동적으로 호출할 수 있다
4. private으로 선언된 필드도 접근해서 값을 읽을 수 있다

###### 예시

Spring 프레임워크나 ORM 도구들은 리플렉션을 사용하여 객체를 생성하고 의존성을 주입한다.

```java
@Component
public class UserService {
    @Autowired
    private UserRepository userRepository;

    public User findUser(Long id) {
        return userRepository.findById(id);
    }
}
```

이 코드에서 Spring은 아래처럼 리플렉션을 사용한다

1. 클래스 스캔 : 스프링은 리플렉션을 사용하여 클래스패스에서 @Component가 붙어 빈으로 등록해야 하는 클래스를 스캔한다
2. 객체 생성 : 해당 클래스의 인스턴스를 생성할 때 리플렉션을 사용한다. 이때 디폴트 생성자가 사용된다.
3. 의존성 주입 : 리플렉션을 통해 @Autowired 어노테이션이 붙은 필드를 찾아내고 적절한 구현체를 주입한다.

```java
public class SimpleSpringContext {
    public Object getBean(String className) throws Exception {
        Class<?> clazz = Class.forName(className);
        
        // 객체 생성 (리플렉션 사용)
        Object instance = clazz.getDeclaredConstructor().newInstance();
        
        // 필드 주입 (리플렉션 사용)
        for (Field field : clazz.getDeclaredFields()) {
            if (field.isAnnotationPresent(Autowired.class)) {
                field.setAccessible(true);
                Class<?> fieldType = field.getType();
                Object fieldInstance = getBean(fieldType.getName());
                field.set(instance, fieldInstance);
            }
        }
        
        return instance;
    }
}
```
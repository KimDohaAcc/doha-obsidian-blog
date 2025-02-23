---
{"dg-publish":true,"permalink":"//sw/vo-value-object/","dgPassFrontmatter":true}
---

데이터의 불변성을 보장하고 비지니스 로직에서 사용되는 데이터 객체

[[공부/SW/DTO(Data Transfer Object)\|DTO(Data Transfer Object)]]와 유사하지만 setter를 가지지 않고 *read-only*특징을 가진다

DTO는 setter를 가지고 있기 때문에 사용하는 중에 값을 변경할 수 있지만,
VO는 사용하는 중에 객체 내부의 값을 변경할 수 없다

```java
public class UserVO {
    private Long id;
    private String username;
    private String email;

    // 생성자
    public UserVO(Long id, String username, String email) {
        this.id = id;
        this.username = username;
        this.email = email;
    }

    // Getter
    public Long getId() {
        return id;
    }

    public String getUsername() {
        return username;
    }

    public String getEmail() {
        return email;
    }

    // equals 및 hashCode 메서드 오버라이딩
    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        UserVO userVO = (UserVO) o;
        return Objects.equals(id, userVO.id) &&
                Objects.equals(username, userVO.username) &&
                Objects.equals(email, userVO.email);
    }

    @Override
    public int hashCode() {
        return Objects.hash(id, username, email);
    }

    // toString 메서드 오버라이딩
    @Override
    public String toString() {
        return "UserVO{" +
                "id=" + id +
                ", username='" + username + '\'' +
                ", email='" + email + '\'' +
                '}';
    }
}

```
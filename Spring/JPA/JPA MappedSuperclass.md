> 인프런 김영한님 자바 ORM 표준 JPA 프로그래밍 - 기본 편 강의 내용 정리

<details>
<summary>ToC</summary>

- [@MappedSupberclass](#mappedsupberclass)
- [🧑🏻‍💻 예시 코드](#-예시-코드)
</details>

---

## @MappedSupberclass

-   **공통 매핑 정보가 필요**할 때 사용한다.
-   상속관계 매핑과는 전혀 관계가 없다.
-   엔티티가 아니기 때문에 테이블과 매핑이 되지않는다.
-   부모 클래스를 상속 받는 **자식 클래스에 매핑 정보만 제공**한다.
-   직접 생성해서 사용할 일이 없으므로 **추상클래스로 쓰는 것을 권장**된다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FxVijm%2FbtrABJIANAK%2FCCHKhCdDQhxSloS8U98fi1%2Fimg.png)

## 🧑🏻‍💻 예시 코드

```java
// BaseEntity.java

@MappedSupercalss
@Getter
public abstract class BaseEntity {
	
    private LocalDateTime createdAt;
    private LocalDateTime modifiedAt;
}
```

```java
// Member.java

@Entity
@Getter
public class Member extends BaseEntity {
	...
}
```
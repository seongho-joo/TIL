> 인프런 자바 ORM 표준 JPA 프로그래밍 - 기본편 강의 내용 정리
<details>
<summaRy>ToC</summary>

- [연관관계 매핑](#연관관계-매핑)
  - [단방향 연관관계](#단방향-연관관계)
  - [양방향 연관관계](#양방향-연관관계)
</details>

---
## 연관관계 매핑
연관관계 매핑이란, **객체의 참조와 테이블의 외래 키를 매핑**하는 것을 말한다.

연관관계는 다음 3가지를 고려해야한다.

1. **방향**(Direction)

방향에는 단방향과 양방이 있다. 객체는 참조용 필드를 가지고 있는 객체만 연관된 객체를 조회할 수 있으므로 방향이 존재한다. 두 객체가 서로 참조하는 관계를 양방향 관계, 한 객체에서 다른 객체만 참조하는 관계를 단방향 객체라 한다.

```java
class A {
    B b;
}

class B {
    A a;
}
```

테이블은 외래 키 하나로 양쪽으로 조인이 가능하다. 따라서 테이블은 방향이 없다고 볼 수도 있고, 항상 양방향이라 할 수 있다.

```java
SELECT *
FROM MEMBER M
JOIN TEAM T ON M.TEAM_ID = T.TEAM_ID
 
SELECT *
FROM TEAM T
JOIN MEMBER M ON T.TEAM_ID = M.TEAM_ID
```

2\. **다중성**(Multiplicity)

연관관계는 다음과 같은 다중성이 있다.

-   일대다(1:N, OneToMany)
-   다대일(N:1, ManyToOne)
-   일대일(1:1, OneToOne)
-   다대다(N:N, ManyToMany)

3\. **연관관계의 주인**(Owner)

연관관계를 관리 포인트는 외래 키인데, 양방향 관계를 맺으면 객체 서로가 외래 키를 가질 수 있게 된다. 따라서 **두 객체 중 하나를 외래 키를 관리**해야 한다. 외래 키를 관리하는 객체를 **연관관계의 주인이라 한다.**

테이블과 객체를 설계할 때 **외래 키를 가지는 엔티티를 연관관계 주인**으로 정하는데, 그 이유는 외래 키를 가진 테이블과 매핑되는 엔티티가 외래 키를 관리하는 것이 효율적이기 때문이다.

**연관관계 주인만이 데이터를 등록, 변경할 수 있으며, 주인이 아닌 객체는 읽기만 가능하다.**

### 단방향 연관관계

_회원과 팀의 관계 예시_

-  회원은 하나의 팀에만 소속된다.
-  팀은 여러 회원들이 존재한다.
-  따라서 회원과 팀은 N:1 관계이다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbuAN31%2Fbtrzthn3LI9%2FzPXZDBaKz9k9GZkOJebpHk%2Fimg.png)

```
@Entity
public class Member {

    @Id @GeneratedValue
    @Column(name = "member_id")
    private Long id;
    
    private String username;
    
    @ManyToOne
    @JoinColumn(name = "team_id")
    private Team team;
}

@Entity
public class Team {
	
    @Id @GeneratedValue
    @Column(name = "team_id")
    private Long id;
    
    private String name;

}
```

-   N:1 연관관계를 맺을 때는 @ManyToOne 애노테이션을 사용한다.
-   외래 키를 매핑할 때는 **@JoinColunm** 애노테이션을 사용하고, **name 옵션에 외래 키 필드 이름을** 넣는다.

### 양방향 연관관계

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbOeAcG%2FbtrzuQXHUh8%2FJdMVzUG9nOCmSOmO6suDf0%2Fimg.png)

```
@Entity
public class Team {
	
    ...
  
    @OneToMany(mappedBy = "team")
    private List<Member> members = new ArrayList<>();
}
```

-   1:N 연관관계일 때는 **@OneToMany** 애노테이션을 사용한다.
-   여기선 미리 단방향으로 연관관계를 맺었기 때문에 Team 엔티티에만 추가하면 된다.
-   양방향일 때 주인이 아닌 엔티티는 **mappedBy** 옵션에 반대쪽 매핑의 필드 이름을 넣는다.

양방향 연관관계 시 주의점

-   **순수 객체 상태를 고려해서 항상 양쪽에 값을 설정해야 한다.**
-   **연관관계 편의 메서드**를 생성하는 것이 좋다.
-   양방향 매핑 시 무한루프를 조심해야 한다.
    -   toString(), lombok, JSON 생성 라이브러리
    -   Controller에서 Entity를 반환하지말고 DTO을 거쳐서 반환해야 한다.

양방향 연관관계 정리 

-   **단반향 매핑만으로 이미 연관관계 매핑은 완료된다.**
-   양방향 매핑은 반대 방향으로 객체 그래프 탐색 기능이 추가된 것이다.
-   단방향 매핑을 잘하고, 양방향은 필요할 때 추가하는 것이 좋다. (테이블에 영향을 주지 않음)
-   **연관관계의 주인은 외래 키의 위치를 기준**으로 정해야 한다.
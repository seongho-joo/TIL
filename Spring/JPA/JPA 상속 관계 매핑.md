> 인프런 자바 ORM 표준 JPA 프로그래밍 - 기본 편 강의 내용 정리

<details>
<summary>ToC</summary>

- [상속 관계 매핑](#상속-관계-매핑)
  - [조인 전략](#조인-전략)
  - [단일 테이블 전략](#단일-테이블-전략)
  - [구현 클래스마다 테이블 전략](#구현-클래스마다-테이블-전략)
</details>

---
## 상속 관계 매핑

관계형 데이터베이스(RDBMS)에서는 객체지향 언어의 상속 개념이 없다.

하지만 슈퍼타입, 서브타입 관계라는 모델링 기법이 객체 상속과 유사하다.

**상속관계 매핑**이란, **객체의 상속 구조와 DB의 슈퍼 타입 서브타입 관계를 매핑**하는 것이다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcJelpn%2FbtrAqJb0ZEJ%2FqhyqtA2wicPW0U2FVt9nPK%2Fimg.png)

슈퍼타입 서브타입 논리 모델을 실제 물리 모델로 구현하는 방법은 다음과 같다.

-  각 테이블로 변환 : 조인 전략 ➡️ 각각 테이블을 만들고 조회할 때 조인
-  통합 테이블로 변환 : 단일 테이블 전략 ➡️ 하나의 테이블에 컬럼들을 모두 통합해서 사용 
-  서브타입 테이블로 변환 : 구현 클래스마다 테이블 전략 ➡️ 서브 타입마다 하나의 테이블로 만듦

객체는 타입이 있지만 테이블은 타입이라는 개념이 없어 하위 클래스를 구분하기 위해서 DTYPE 컬럼을 따로 추가해야 줘야 한다.

상속 매핑 주요 애노테이션

- **@Inheritance**
  -  strategy 옵션을 사용하여 전략을 지정한다.
  -  InheritanceType 종류
     - JOINED: 조인 전략
     - SINGLE_TABLE: 단일 테이블 전략
     - TABLE_PER_CLASS: 구현 클래스마다 테이블 전략
- **@DiscriminatorColumn(name = "DTYPE")**
  - 부모 클래스에 선언
  - 하위 클래스를 구분하는 용도의 컬럼
- **@DiscriminatorValue("name")**
  - 하위 클래스에 선언
  - 엔티티를 저장할 때 슈퍼 타입의 구분 컬럼에 저장할 값을 지정
  - 애노테이션을 선언하지 않을 경우 기본 값은 클래스 이름이다.

### 조인 전략

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FVEf15%2FbtrAqS7w3CB%2FtEfgcsWrXTEofwvQpWxRa1%2Fimg.png)

```java
// Item 엔티티
@Entity
@Inheritance(strategy = InheritanceType.JOINED)
@DiscriminatorColumn(name = "DTYPE")
public abstract class Item{
	@Id @GeneratedValue
	@Column(name = "ITEM_ID")
	private Long id;
	
	private String name;
	private int price;
}

// Album 엔티티
@Entity
@DiscriminatorValue("A")
public class Album extends Item{
	private String artist;
}

// Movie 엔티티
@Entity
@DiscriminatorValue("M")
public class Movie extends Item{
	private String director;
	private String actor;
}
```

가장 정규화된 방법으로 구현하는 방식이다. 각 엔티티를 테이블로 만들기 때문에 저장 공간이 효율적이다.

부모 엔티티의 PK를 PK + FK로 사용한다.  조회할 때는 조인을 사용하고, FK 참조 무결성 제약조건을 활용할 수 있다. 

조회 시 조인을 많이 사용하므로 성능이 저하될 수 있고, 조회 쿼리가 복잡하다. 데이터 저장 시 INSERT SQL을 2번 호출한다.

### 단일 테이블 전략

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbOZbaz%2FbtrAqIqE1ID%2FR11rZxWMqKuCCwZkD4BLSk%2Fimg.png)

```java
// Item 엔티티
@Entity
@Inheritance(strategy = InheritanceType.SINGLE_TABLE)
@DiscriminatorColumn(name = "DTYPE")
public abstract class Item{
	@Id @GeneratedValue
	@Column(name = "ITEM_ID")
	private Long id;
	
	private String name;
	private int price;
}

// Album 엔티티
@Entity
@DiscriminatorValue("A")
public class Album extends Item{
	private String artist;
}

// Movie 엔티티
@Entity
@DiscriminatorValue("M")
public class Movie extends Item{
	private String director;
	private String actor;
}
```

서비스 규모가 크지 않을 때 주로 사용한다.

한 테이블에 모든 컬럼들을 넣어서 사용하기 때문에 조인할 필요가 없다. 따라서 일반적으로 조회 성능이 빠르고 조회 쿼리가 아주 간단하다.

하지만 자식 엔티티가 매핑한 컬럼은 모두 null 허용이 되고, 단일 테이블에 모든 것을 저장하므로 서비스 규모가 커진다면 조회 성능이 떨어질 수 있다.

### 구현 클래스마다 테이블 전략

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FO8O9M%2FbtrArebPBJu%2Frt2C4uCo5UcbsB8H9gTnjK%2Fimg.png)

```java
// Item 엔티티
@Entity
@Inheritance(strategy = InheritanceType.TABLE_PER_CLASS)
@DiscriminatorColumn(name = "DTYPE")
public abstract class Item{
	@Id @GeneratedValue
	@Column(name = "ITEM_ID")
	private Long id;
	
	private String name;
	private int price;
}

// Album 엔티티
@Entity
@DiscriminatorValue("A")
public class Album extends Item{
	private String artist;
}

// Movie 엔티티
@Entity
@DiscriminatorValue("M")
public class Movie extends Item{
	private String director;
	private String actor;
}
```

서브 타입을 명확하게 구분해서 처리할 때 효과적이고 not null 제약조건 사용이 가능하다. 하지만 자식 테이블을 통합해서 쿼리 하기 어렵고 여러 하위 테이블을 함께 조회할 때 UNION SQL이 필요하므로 성능이 매우 느리다. 따라서 이 전략은 실무에서 사용되지 않는다.
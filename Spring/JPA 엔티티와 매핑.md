<details>
<summay>ToC</summary>

- [엔티티와 매핑](#엔티티와-매핑)
- [@Entity](#entity)
  - [속성](#속성)
  - [❗️주의사항❗️](#️주의사항️)
- [@Table](#table)
- [데이터베이스 스키마 자동 생성](#데이터베이스-스키마-자동-생성)
  - [❗️주의사항❗️](#️주의사항️-1)
- [필드와 컬럼 매핑](#필드와-컬럼-매핑)
  - [@Column](#column)
  - [@Enumerated](#enumerated)
  - [@Temoral](#temoral)
  - [@Lob](#lob)
  - [@Transient](#transient)
- [기본 키 매핑](#기본-키-매핑)
  - [IDENTITY 전략](#identity-전략)
  - [SEQUENCE 전략](#sequence-전략)
  - [TABLE 전략](#table-전략)

</details>

## 엔티티와 매핑
- 객체와 테이블 매핑 : `@Entity`, `@Table`
- 필드와 컬럼 매핑 : `@Column`
- 기본 키 매핑: `@Id` 
- 연관관계 매핑: `@ManyToOne`, `@JoinColumn`

## @Entity
- 테이블과의 매핑
- `@Entity`가 붙은 클래스는 JAP가 관리하며, 엔티티라 불린다.

### 속성
- name
  - JPA에서 사용할 엔티티 이름을 지정
  - 기본값은 클래스 이름이고 가급적 기본값을 사용

### ❗️주의사항❗️
- **기본 생성자는 반드시 존재해야함**
- `final` 클래스, `enum`, `interface`, `inner` 클래스에서는 사용할 수 없음
- 저장할 필드에 `final` 사용 불가

## @Table
- 엔티티와 매핑할 테이블 지정

속성|기능|기본값
--|--|--
name|매핑할 테이블 이름|엔티티 이름을 사용
catalog|DB catalog 매핑|
schema|DB schema 매핑|
uniqueConstraints(DDL)|DDL 생성시에 유니크 제약 조건 생성

## 데이터베이스 스키마 자동 생성
- DDL을 애플리케이션 실행 시점에 자동 생성
- 데이터베이스 방언을 활용해서 데이터베이스에 맞는 적절한 DDL 생성
- **DDL 생성기능은 DDL을 자동 생성할 때만 사용되고 JPA 실행 로직에는 영향을 주지 않음**

`yml` 기준 `ddl-auto` 속성 추가
```yml
spring:
    jpa:
        hibernate:
            ddl-auto: create
```
옵션|설명
--|--
create|기존 테이블 삭제 후 생성
create-drop| create와 같으나 종료 시점에 테이블 DROP
update|변경분만 반영
validate|엔티티와 테이블이 정상 매핑 되었는지 확인하고 정상적으로 매핑이 되지않았다면 애플리케이션을 실행하지 않음
none|사용하지 않음

### ❗️주의사항❗️
- **운영 장비에서는 절대 create, create-drop, update를 사용하면 안됨**
- 개발 초기 단계는 create 또는 update
- 테스트 서버는 update 또는 validate
- 스테이징과 운영 서버는 validate 또는 none

## 필드와 컬럼 매핑

어노테이션 | 설명
-- | --
@Column | 컬럼 매핑
@Temporal | 날짜 타입 매핑
@Enumerated | enum 타입 매핑
@Lob | BLOB, CLOB 매핑
@Transient | 특정 필드를 컬럼에 매핑하지 않음

### @Column
- 객체 필드를 테이블 컬럼에 매핑
- name, nullable를 제외하곤 잘 사용하지 않음

속성 | 설명 | 기본값
-- | -- | --
name | 필드와 매핑할 테이블의 컬럼이름 | 객체의 필드 이름
insertable | 엔티티 저장 시 이 필드도 같이 저장 | true
updatable | 엔티티 수정 시 이 필드도 같이 수정 | true
nullable(DDL) | null 값의 허용 여부를 설정 | true
unique(DDL) | @Table의 uniqueConstraints와 같지만 한 컬럼에 간단한 유니크 제약조건을 걸 때 사용 | 
columnDefinition(DDL) | 데이터 컬럼 정보를 직접 줄 수 있음 | 필드의 자바 타입과 방언 정보를 사용
length(DDL) | 문자 길이 제약조건, String 타입에만 사용 | 255
precision, scale(DDL) | BiDecimal 타입에서 사용<br/> precision은 소수점을 포함한 전체 자릿수, scale은 소수의 자릿수 (참고: double, float 타입에는 적용되지 않고, 아주 큰 숫자나 정밀한 소수를 다루어야 할 때만 사용) | precision=19<br/>scale=2

### @Enumerated
- 자바 enum 타입을 매핑할 때 사용

| 속성 | 설명 | 기본값 |
| --- | --- | --- |
| value | - EnumType.ORDINAL : enum 순서를 데이터베이스에 저장<br/>- EnumType.STRING : enum 이름을 데이터베이스에 저장 | EnumType.ORDINAL |

### @Temoral
- 날짜 타입을 매핑할 때 사용
- `LocalDate`, `LocalDateTime`을 사용할 때는 생략 가능

| 속성 | 설명 | 기본값 |
| --- | --- | --- |
| value |   **TemporalType.DATE**: 날짜, 데이터베이스 date 타입과 매핑 (예: 2013–10–11) <br/>**TemporalType.TIME**: 시간, 데이터베이스 time 타입과 매핑  (예: 11:11:11)  <br/>**TemporalType.TIMESTAMP**: 날짜와 시간, 데이터베이스  timestamp 타입과 매핑(예: 2013–10–11 11:11:11)         |   |

### @Lob
- 데이터베이스 BLOB, CLOB 타입과 매핑
  - @Lob에는 지정할 수 있는 속성이 없음
  - 매핑하는 필드 타입이 문자면 CLOB 매핑, 나머지는 BLOB 매핑
    - CLOB : String, char[], java.sql.CLOB
    - BLOB : byte[], java.sql.BLOB

### @Transient
- 필드 매핑을 하지않음 ➡️ DB에 저장도 하지않고 조회도 안됨
- 주로 메모리상에서만 임시로 어떤 값을 보관하고 싶을 때 사용

```java
@Transient
private Integer temp;
```

## 기본 키 매핑
- 직접 할당: `@Id` 애노테이션을 사용하여 개발자가 직접 할당
- 자동 생성: 대리 키 사용 방식(`@GeneratedValue` 애노테이션 사용)
  - IDENTITY: 데이터베이스에 위임
  - SEQUENCE: 데이터베이스 시퀀스 오브젝트 사용
  - TABLE: 키 생성용 테이블 사용, 모든 DB에서 사용
  - AUTO: 방언에 따라 자동 지정, 기본값

**권장하는 식별자 전략**
- 기본 키 제약 조건 : null이 아니어야하고, 유일해야하고, 변하면 안된다.
- 권장 : Long형 + 대체 키 + 키 생성전략 사용

### IDENTITY 전략
- 기본 키 생성을 데이터베이스에 위임
- auto_increment는 DB에 intsert sql을 실행한 이후에 PK값을 알 수 있음
```java
@Entity
public class Member {
  @Id
  @GeneratedValue(strategy = GenerationType.IDENTITY)
  private Long id;
}
```

### SEQUENCE 전략
- 데이터베이스 시퀀스는 유일한 값을 순서대로 생성하는 특별한 데이터베이스 오브젝트

속성| 설명| 기본값
--|--|--
name|식별자 생성기 이름|필수|
sequenceName|데이터베이스에 등록되어 있는 시퀀스 이름|hibernate_sequence|
initialValue|DDL 생성 시에만 사용됨, 시퀀스 DDL을 생성할 때 처음 1 시작하는 수를 지정한다.|1|
allocationSize|시퀀스 한 번 호출에 증가하는 수(성능 최적화에 사용됨 데이터베이스 시퀀스 값이 하나씩 증가하도록 설정되어 있으면 이 값 을 반드시 1로 설정해야 한다 | 50|
catalog, schema|데이터베이스 catalog, schema 이름|

```java
@Entity
@SequenceGenerator(
    name = "MEMBER_SEQ_GENERATOR",
    sequenceName = "MEMBER_SEQ", //매핑할 데이터베이스 시퀀스 이름
    initialValue = 1, allocationSize = 1)
public class Member {
    @Id
    @GeneratedValue(strategy = GenerationType.SEQUENCE, generator = "MEMBER_SEQ_GENERATOR")
    private Long id;
}
```

### TABLE 전략
- 키 생성 전용 테이블을 하나 만들어서 데이터베이스 시퀀스를 흉내내는 전략
- 모든 데이터베이스에 적용가능하다는 장점이 있지만 성능이 떨어지는 단점이 있다.

```sql
create table MY_SEQUENCES (
    sequence_name varchar(255) not null,
    next_val bigint,
    primary key ( sequence_name )
)
```
```java
@Entity
@TableGenerator(
    name = "MEMBER_SEQ_GENERATOR",
    table = "MY_SEQUENCES",
    pkColumnValue = "MEMBER_SEQ", allocationSize = 1)
public class Member {
    @Id
    @GeneratedValue(strategy = GenerationType.TABLE, generator = "MEMBER_SEQ_GENERATOR")
    private Long id;
}
```

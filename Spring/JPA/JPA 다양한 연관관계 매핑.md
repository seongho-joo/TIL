> 인프런 자바 ORM 표준 JPA 프로그래밍 - 기본편 강의 내용 정리

---

## 다양한 연관관계 매핑

-   다대일(N:1, @ManyToOne) ⬌ 일대다(1:N, @OneToMany)
-   일대일(1:1, @OneToOne)
-   다대대(N:M @ManyToMany)

## 다대일(@ManyToOne)  - 단방향

[##_Image|kage@uCFSC/btrzYEiX0bY/2CyyObtLbHKete0rNziN90/img.png|CDM|1.3|{"originWidth":897,"originHeight":468,"style":"widthContent","caption":"다대일 단방향 - 객체 테이블 설계"}_##]

-   가장 많이 사용하는 연관관계이며, 반대는 일대다이다.

## 다대일(@ManyToOne)  - 양방향

[##_Image|kage@Hxkn4/btrzYht5B2O/UYjeyrsBqJledPPosxyzOK/img.png|CDM|1.3|{"originWidth":916,"originHeight":542,"style":"widthContent","caption":"다대일 양방향 - 객체 테이블 설계"}_##]

-   FK가 있는 쪽이 연관관계의 주인
-   양쪽을 서로 참조하도록 개발

## 일대다(@OneToMany) - 단방향

[##_Image|kage@bXJzLk/btrzYTNK6Sc/JfrvudYde5i77rRmXOQ9iK/img.png|CDM|1.3|{"originWidth":964,"originHeight":542,"style":"widthContent","caption":"일대다 단방향 - 객체와 테이블 설계"}_##]

-   일대다 단방향은 **일이 연관관계의 주인**
-   테이블 일대다 관계는 **항상 다쪽에 FK가 있음**
-   객체와 테이블의 차이 때문에 반대편 테이블의 외래 키를 관리하는 특이한 구조
-   **@JoinColumn을 꼭 사용해야 함.** 그렇지 않으면 JoinTable방식을 사용해서 중간에 테이블을 하나 추가됨
-   단점
    -   엔티티가 관리하는 FK가 다른 테이블에 존재함
    -   연관관계 관리를 위해 추가로 UPDATE SQL를 실행함
    -   따라서 일대다 단방향보다는 **다대일 양방향 매핑을 사용**하는 것이 좋음

## 일대다(@OneToMany) - 양방향

[##_Image|kage@bT8Tyx/btrz3P4fFd7/BI5xnWPkIAJSaC9cgyXIc0/img.png|CDM|1.3|{"originWidth":1054,"originHeight":544,"style":"widthContent","caption":"일대다 양방향 - 객체와 테이블 설계"}_##]

-   일대다 양방향은 공식적으로 제공하지 않는다.
-   @JoinColumn(insertable = false, updatable = false)와 같이 옵션을 설정하고 **읽기 전용 필드**를 사용해서 양방형처럼 사용한다.

## 일대일(@OneToOne) 관계

-   주 테이블이나 대상 테이블 중에 FK 선택이 가능하다.
    -   주 테이블 : access가 많은 테이블
-   FK에 데이터베이스 유니크 제약조건을 추가해야 한다.

### 주 테이블 FK 단방향

[##_Image|kage@z3Qai/btrz45yQOEW/IPoP4XE5hR84GokvCS2WYK/img.png|CDM|1.3|{"originWidth":1054,"originHeight":544,"style":"alignCenter","caption":"일대일 단방향 - 객체와 테이블 설계"}_##]

-   다대일 단방향 매핑과 유사하다.

### 주 테이블 FK 양방향

[##_Image|kage@cNzxrR/btrz34ApDT7/G32gsAXrDLkez15EoXcxdK/img.png|CDM|1.3|{"originWidth":950,"originHeight":544,"style":"alignCenter","caption":"일대일 양방향 - 객체와 테이블 설계"}_##]

-   다대일 양방향 매핑처럼 FK가 있는 곳이 연관관계의 주인이다.

### 대상 테이블 FK 단방향

-   대상 테이블을 연관관계의 주인으로 지정할 경우는 JPA에서 지원하지 않는다.

### 대상 테이블 FK 양방향

[##_Image|kage@cCHTls/btrz0ufh8eQ/D2hMkbKFGmCWEhQSitGG7K/img.png|CDM|1.3|{"originWidth":950,"originHeight":544,"style":"alignCenter","caption":"일대일 양방향 - 객체와 테이블 설계"}_##]

-   다대일 양방향 매핑과 유사하다.

#### 주 테이블 FK

-   주 객체가 대상 객체의 참조를 가지는 것처럼 주 테이블에 FK를 두고 대상 테이블을 찾는다.
-   객체지향 개발자가 선호하는 방식이다.
-   JPA 매핑이 편리하다.
-   주 테이블만 조회해도 대상 테이블에 데이터가 있는지 확인이 가능하다.
-   대상 테이블에 값이 없으면 FK에 null이 허용되는 단점이 있다.

#### 대상 테이블 FK

-   대상 테이블에 FK가 존재한다.
-   전통적인 데이터베이스 개발자가 선호하는 방식이다.
-   주 테이블과 대상 테이블을 일대일에서 일대다 관계로 변경할 때 테이블 구조를 그대로 유지할 수 있다.
-   프록시 기능의 한계로 **지연 로딩으로 설정해도 항상 즉시 로딩**이 된다는 단점이 있다.

## 다대다(@ManyToMany)

[##_Image|kage@m4myI/btrz34HekoS/IJF9LX0X00kTQjiTHVc27k/img.png|CDM|1.3|{"originWidth":950,"originHeight":408,"style":"alignCenter","caption":"다대다 테이블 설계"}_##][##_Image|kage@cqmvpS/btrz3PpIsku/EFScWXwljxxwLU1QSwSZak/img.png|CDM|1.3|{"originWidth":950,"originHeight":408,"style":"alignCenter","caption":"다대다 테이블 설계"}_##]

-   RDBMS는 정규화된 테이블 2개를 다대다 관계를 표현할 수 없다.
-   다대다로 관계를 맺을 때는 연결 테이블을 추가해서 다대일, 일대다 관계로 풀어내야 한다.
-   **객체는 컬렉션을 사용해서 객체 2개로 다대다 관계가 가능하다.**
-   @ManyToMany 애노테이션을 사용하며, @JoinTable로 연결 테이블을 지정해야 한다.
-   연결 테이블에 다른 필드들이 추가될 수 있으므로 실무에선 사용하지 않는다.
-   실무에서 다대다 관계는 **연결 테이블용 엔티티를 추가**하여 사용한다.

[##_Image|kage@Ezddt/btrz4317nHV/CmnuDk3Ovl9OKX6v6P6wQk/img.png|CDM|1.3|{"originWidth":1060,"originHeight":414,"style":"alignCenter","caption":"실무에서 사용하는 다대다(1:N N:1) 테이블 설계","filename":"스크린샷 2022-04-21 오후 2.52.48.png"}_##]

## 🔗 실습 예제

 [feat: delivery, category 엔티티 추가 및 연관관계 매핑 · seongho-joo/jpa-basic@7dc3e99

This commit does not belong to any branch on this repository, and may belong to a fork outside of the repository.

github.com](https://github.com/seongho-joo/jpa-basic/commit/7dc3e997bcb9089dd50aa5ab779183b8daf8f552)
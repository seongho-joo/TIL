# NSLayoutConstraint

### NSLayoutConstraint
- 오토레이아웃 방정식
    view1.attr1 = view2.attr2 * multiplier + constant
    item.attribute = toltem.attribut * multiplier +  constant

매개변수|설명|비고
---|---|---
item|제약조건을 받는 왼쪽 뷰|
relatedBy|제약조건을 받는 뷰 간의 관계|`NSLayoutConstraint` 열겨형 값을 가짐 <br> (.lessThanOrEqual, .equal, .greaterThanOrEqual)
attribute|왼쪽 뷰의 제약조건의 속성|`NSLayoutConstraint` 열겨형 값을 가짐 <br> (.left, .right, .top, .bottom, .leading, .trailing, .width, .height, .centerX, centerY, .lastBaseline, .notAnAttribute 등)
toltem|왼쪽 뷰의 제약조건을 받을 오른쪽 뷰|없을 경우 `nil` 가능
attribute|오른쪽 뷰의 제약조건의 속성|`NSLayoutConstraint` 열겨형 값을 가짐 <br> (.left, .right, .top, .bottom, .leading, .trailing, .width, .height, .centerX, centerY, .lastBaseline, .notAnAttribute 등)
multiplier|왼쪽 뷰의 속성값을 얻기 위해 오른쪽 뷰의 속성값을 곱함|이 값을 이용해 비율로 크기를  설정할 수 있고, 위치지정에도 활용할 수 있음
constant|상수 값|비율의 값이 아닌 상수의 값이 필요한 경우 사용

### Visual Format Language

기호 및 문자열| 설명
---|---
\||superView
\-|표준 간격, default는 8포인트
==|같은 너비
-x-|사이의 간역이 x포인트
<=x|x보다 작거나 같음
\>=x|x보다 크거나 같음
@|우선도 지정
H|수평 방향(가로)
V|수직 방향(세로)

[사용 예시](https://www.edwith.org/boostcourse-ios/lecture/16849/)
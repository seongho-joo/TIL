# 컴포넌트

- 함수형 컴포넌트
  - 선언하기 편함
  - 메모리 자원을 클래스형 보다 덜 사용
  - Hooks라는 기능을 통해 라이프사이클 API 사용 가능
- 클래스형 컴포넌트
  - state 기능 및 라이프사이클 기능 사용 가능

- props
  - properties를 줄인 표현
  - 컴포넌트 속성을 설정할 때 사용하는 요소

- Children
  - 태그 사이에 값을 보여주는 props
  - 컴포넌트 내부에서 보여 줄려면 `porps.children`을 사용
```
// App.js
import React from 'react';
import MyComponent from './MyComponent';

const App = () => {
    return <MyComponent>Children</MyComponent>;
}

export default App;

// MyComponent.js
import React from 'react';

const MyComponent = (props) => {
  return (
      <div>
        props 값 : {props.name}<br/>
        children 값 : {props.children}
      </div>
  );
};

MyComponent.defalutProps = {
    name: '기본 이름'
};

export default MyComponent;
```

- propsTypes
  - 컴포넌트의 필수 props를 지정하거나 props의 타입을 지정할 때 사용
  - `isRequried`를 사용하여 필수 propTypes를 설정
  - 종류
    - array
    - arrayOf : 특정 PropType으로 이루어진 배열
    - bool
    - func
    - number
    - object
    - string
    - symbol
    - node : 렌더링할 수 있는 모든 것
    - instanceOf : 특정 클래스의 인스턴스
    - oneOf : 주어진 배열 요소 중 값 하나
    - oneOfType
    - objectOf
    - shape : 주어진 스키마를 가진 객체
    - any
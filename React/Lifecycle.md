# 라이프사이클

## 라이프사이클 메서드
- Will~ 어떤 작업을 작동하기 전에 실행되는 메서드
- Did~ 어떤 작업을 작동한 후에 실행되는 메서드
- 마운트, 업데이트, 언마운트 세 가지가 있음

### 마운트
- DOM이 생성되고 웹 브라우저상에 나타나는 것
- 메서드 종류
  - `constructor` : 컴포넌트를 새로 만들 때마다 호출되는 클래스 생성자 메서드
  - `getDerivedStateFromPorps` : props에 있는 값을 state에 넣을 때 사용하는 메서드
  - `render` : 우리가 준비한 UI를 렌더링하는 메서드
  - `componentDidMount` : 컴포넌트가 웹 브라우저상에 나타난 후 호출하는 메서드

### 업데이트
- 업데이트를 발생시키는 요인
  - props 변경
  - state 변경
  - 부모 컴포넌트 리렌더링
  - `this.forceUpdate`로 강제 렌더링 트리거
  - 메서드 종류
    - `getDerivedStateFromPorps` : 마운트 과정과 동일
    - `shouldComponentUpdate` : 컴포넌트가 리렌더링을 해야 할지 말아야 할지를 결정하는 메서드
    - `render` : 컴포넌트 리렌더링
    - `getSnapshotBeforeUpdate` : 컴포넌트 변화를 DOM에 반영하기 바로 직전에 호출되는 메서드
    - `componentDidUpdate` : 컴포넌트의 업데이트 작업이 끝난 후 호출하는 메서드

### 언마운트
- 마운트의 반대 과정, 즉 컴포넌트를 DOM에서 제거하는 것
- `componentWillUnmout` : 컴포넌트가 웹 브라우저상에서 사라지기 전에 호출하는 메서드
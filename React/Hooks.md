# Hooks

## Hooks
- 리액트 v16.8에 새로 도입된 기능
- 함수형 컴포넌트에서 상태관리와 렌더링 직후 작업 설정 등 기능 제공

- `useState`
  - 가장 기본적인 Hook이며, 함수형 컴포넌트에서 가변적인 상태를 지닐 수 있게 함
  - 하나의 `useState` 함수는 하나의 상태 값만 관리할 수 있음 -> 관리할 상태가 여러개라면 `useState`를 여러번 사용
    ```
    import React, { useState } from 'react';

    const Counter = () => {
        const [value, setValue] = useState(0);
        return (
            <div>
                <p>
                    현재 값 <b>{value}</b>
                </p>
                <button onClick={() => setValue(value + 1)}> + 1 </button>
                <button onClick={() => setValue(value - 1)}> - 1 </button>
            </div>
        );
    };

    export default Counter;
    ```

- `useEffect`
  - 리액트 컴포넌트가 렌더일될 때마다 특정 작업을 수행하도록 설정할 수 있는 Hook
  - `componentDidMount`와 `componentDidUpdate` 기능 수행
  ```
  useEffect(() = > {
      console.log('렌더링될 때마다 실행')
  })

  useEffect(() => {
      console.log('마운트될 때만 실행')
  }, [])

  useEffect(() => {
      console.log('특정 값이 업데이트될 때만 실행')
  }, [name])
  ```

- `useReducer`
  - `useState`보다 더 다양한 컴포넌트 상황에 따라 다양한 상태를 다른 값으로 업데이트 해주고 싶을 때 사용하는 Hook
  - 현재 상태, 그리고 업데이트를 위해 필요한 정보를 담은 액션값을 전달받아 새로운 상태를 반환
  - 리듀서 함수에서 새로운 상태를 만들 때는 반드시 불변성을 지켜야함
  - 액션 객체에는 어떤 액션인지 알려주는 type 필드 필요
  ```
  import React, { useReducer } from 'react';

  function reducer(state, action) {
      switch (action.type) {
          case 'INCREMENT':
              return { value: state.value + 1 };
          case 'DECREMENT':
              return { value: state.value - 1 };
          default:
              return state;
      }
  }

  const Counter = () => {
      const [state, dispatch] = useReducer(reducer, { value: 0 });
      return (
          <div>
              <p>
                  현재 값 <b>{state.value}</b>
              </p>
              <button onClick={() => dispatch({ type: 'INCREMENT' })}>+ 1</button>
              <button onClick={() => dispatch({ type: 'DECREMENT' })}>- 1</button>
          </div>
      );
  };

  export default Counter;
  ```

- `useMemo`
  - 함수형 컴포넌트 내부에서 발생하는 연산을 최적화 함
  - 렌더링하는 과정에서 특정 값이 바뀌었을 때만 연산 실행

- `useCallback`
  - 렌더링 성능을 최적화해야 하는 상황에서 사용
  - 함수를 새로 만들지 않고 재사용 가능
  - 비어있는 배열을 파라미터로 넣으면 렌더링될 때 함수를 새로 생성
  - data가 있는 배열을 파라미터로 넣으면 input 내용이 바뀌거나 새로운 항목이 추가될 때 함수 새로 생성

- `useRef`
  - 함수형 컴포넌트에서 ref를 쉽게 사용할 수 있도록 해줌
# State

- State
  - 리액트에서 state는 컴포넌트 내부에서 바뀔 수 있는 값을 의미
  - state의 값을 변경하면 리렌더링 됨.
  - state의 값을 변경할때 `setState` 또는 `useState`를 통해 전달받은 세터 함수를 사용해야함.

- 클래스형 컴포넌트
```
import React, { Component } from 'react';

class Counter extends Component {
    state = {
        number: 0,
        fixedNumber: 0,
    };
    render() {
        const { number, fixedNumber } = this.state;
        return (
            <div>
                <h1>{number}</h1>
                <h2>상수 {fixedNumber}</h2>
                <button
                    onClick={() => {
                        this.setState({ number: number + 1 }, () => {
                            console.log('setState가 호출됨');
                            console.log(this.state);
                        });
                    }}
                >
                    +1
                </button>
            </div>
        );
    }
}

export default Counter;

```
- 함수형 컴포넌트
  -  리액트 16.8 이후 부터 `useState`라는 함수를 사용하여 state를 사용할 수 있음
```
import React, { useState } from 'react';

const Say = () => {
    // 배열 비구조화 할당
    const [message, setMessage] = useState('');
    const onClickEnter = () => setMessage('hello');
    const onClickLeave = () => setMessage('bye');
    return (
        <div>
            <button onClick={onClickEnter}>입장</button>
            <button onClick={onClickLeave}>퇴장</button>
            <h1>{message}</h1>
        </div>
    );
};

export default Say;

```
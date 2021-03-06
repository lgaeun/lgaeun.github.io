---
title: "☀️ 3/13 React - contextAPI, useReducer"
date: 2022-03-13 9:32:00 +0900
categories: [TIL]
tags: [React]
---

### ContextAPI

- props drilling을 방지하기 위한 방법 중 하나
- 1 context 1 content ⇒ 즉, 여러 데이터를 넘기기 위해서는
  - context를 데이터 갯수 만큼 생성하던가
  - 객체를 value로 넘기기 (better!)
- contextAPI 자체는 state 관리가 아님. useState나 dispatch를 함께 사용한다면 상태관리가 될 수 있음.

1. useContext를 이용해 클릭하면 커지는 원 구현하기

```jsx
import React, { useState, useContext } from "react";
import logo from "./logo.svg";
import "./App.css";

const CircleSizeContext = React.createContext();

function CircleSizeProvider(props) {
  const [circleSize, circleSizeChange] = useState(20);
  return (
    <CircleSizeContext.Provider value={% raw %}{{ circleSize, circleSizeChange }}{% endraw %}>
      {props.children}
    </CircleSizeContext.Provider>
  );
}

function Circle() {
  const { circleSize, circleSizeChange } = useContext(CircleSizeContext);

  return (
    <div
      onClick={() => circleSizeChange(circleSize + 20)}
      style={% raw %}{{
        width: circleSize + "px",
        height: circleSize + "px",
        borderRadius: "50%",
        background: "red",
      }}{% endraw %}
    />
  );
}

function App() {
  return (
    <CircleSizeProvider>
      <div className="App">
        <h1>Click circle</h1>
        <div style={% raw %}{{ display: "flex", justifyContent: "center" }}{% endraw %}>
          <Circle />
        </div>
      </div>
    </CircleSizeProvider>
  );
}

export default App;
```

### useReducer

useState → 상태관리라는 것을 할 수 있다

useReducer → 상태관리를 조금 다른 방법으로 할 수 있다.

```jsx
import React, { useReducer } from "react";
import logo from "./logo.svg";
import "./App.css";

// reducer: (현재 상태, '액션' 객체)를 받아서 -> 새로운 상태를 반환
// action: 업데이트를 위한 정보를 갖고 있다.
// state: component에서 사용할 상태 자체를 의미
// dispatch: '액션'을 발생시키는 함수

const [state, dispatch] = useReducer(reducer, initialState);

function reducer(state, action) {
  switch (action.type) {
    case "INCREMENT":
      return state + 1;
    case "DECREMENT":
      return state - 1;
    default:
      return state;
  }
}

function Counter() {
  const [number, dispatch] = useReducer(reducer, 0);

  const onIncrease = () => {
    dispatch({ type: "INCREMENT" });
  };

  const onDecrease = () => {
    dispatch({ type: "DECREMENT" });
  };

  return (
    <div>
      <h1>{number}</h1>
      <button onClick={onIncrease}>+1</button>
      <button onClick={onDecrease}>-1</button>
    </div>
  );
}

function App() {
  return (
    <div className="App">
      <Counter />
    </div>
  );
}

export default App;
```

useReducer

- 장점
  - 코드의 가독성이 올라간다
  - 다양한 케이스에 대해 대응이 가능해진다
- 단점
  - 코드의 길이가 늘어난다

### 그렇다면 useState와 useReducer 중에 뭘 쓰면 좋을까?

각자 상황, 구현하고자는 컴포넌트의 구조에 따라 다르겠지만 대체적으로

→ useState: 컴포넌트에서 관리하는 값이 적고, 구조가 단순한 경우

→ useReducer: 상태의 구조가 복잡할 때 사용하면 유리하다

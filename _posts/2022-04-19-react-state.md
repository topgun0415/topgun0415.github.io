---
layout: post
title: React 'State' ⚛️
date: 2022-04-19 22:00 +0800
# last_modified_at: 2022-02-16 01:08:25 +0800
tags: [react]
toc: true
math: false
---

![React](https://ms314006.github.io/static/b7a8f321b0bbc07ca9b9d22a7a505ed5/97b31/React.jpg)

## 🌀 What is React 'State' ?

### State === 상태

인간에게는 배고픔, 적당함, 배부름 이라는 상태가 존재한다. 사람은 이렇게 3개의 상태에 따라서 행동도 다르게 된다.

즉 <mark>계속해서 변화하는 특정 상태, 상태에 따라 각각 다른 동작을 함</mark>

![Statebutton](https://cdn.dribbble.com/users/3482593/screenshots/6844698/switch.gif)

위의 사진은 요즘 유행하는 다크테마이다. 이것도 Dark 이거나 Light로 클라이언트가 상태를 직접 조작할 수 있게 만든 기능이다.

리액트의 상태는 컴퍼넌트가 갖는 테마처럼 계속 값이 바뀔 동적인 데이터이고, 상태를 바꾸는 등의 관리는 그 기능을 가진 컴퍼넌트가 직접 관리하게 된다.

그럼 이제 예시로 알아보겠다.

### 에시

<mark>App Component</mark>

```react
import React from "react";
import './App.css';
import MyHeader from "./MyHeader.jsx";
import Counter from "./Counter.jsx";
import Container from "./Container.jsx";

function App() {

  return (
    <Container>
      <div className="App">
        <MyHeader />
        <Counter Value={2}/>
        {/* 이렇게 속성값으로 props라는 값을 전달할 수도 있음 */}
      </div>
    </Container>
  );
}

export default App;
```

<mark>Counter Component</mark>

```react
/** @format */
import React, { useState } from 'react';
import OddEvenResult from './oddEvenResult';

const Counter = () => {
  const [count, setCount] = useState(counterValue3); // props 매개변수로 받아 프로퍼티로 전달 방법

  const onIncrease = () => {
    setCount(count + 1);
  };

  const onDecrease = () => {
    setCount(count - 1);
  };

  return (
    <div>
      <h2>{count}</h2>
      <button onClick={onIncrease}>+</button>
      <button onClick={onDecrease}>-</button>
      <br />
      <OddEvenResult className='result' count={count} />
    </div>
  );
};

Counter.defaultProps = {
  counterValue3: 0,
};

export default Counter;
```

위의 코드는 숫자 데이터인 count을 +와 -의 버튼으로 1씩 더하거나 빼거나 하는 기능이다.

간단하지만 이보다 더 좋은 State 즉 상태를 나타내는 예시는 없다. 이 count는 Counter component의 하위 component들에게 Props으로 count 값을 줄 수도 있으며 이 값은 각 component 끼리 유기적으로 상태를 공유하게 된다.

⛔️ 다만!! 자바스크립트에서 변수를 선언해 데이터를 넣고 계속 다른 값을 넣어 사용했더라면 리액트는 count의 상태를 변경하기 위해서는 setCount로만 접근을 해야한다. 자바나 다른 언어들의 getter, setter 와 같은 기능으로 보면 될거 같다.

### 🆘 Props와 State의 차이

![ReactvsProps](https://res.cloudinary.com/practicaldev/image/fetch/s--xKWyj8SG--/c_imagga_scale,f_auto,fl_progressive,h_500,q_auto,w_1000/http://live-linguine-code.pantheonsite.io/wp-content/uploads/2019/03/react-state-vs-props.jpg)

<mark>Props(Properties)</mark>

1. Arguments of function
2. 컴포넌트 밖에 있다.
3. 수를 카운트하는 앱을 만든다고 했을때 initial value같은 것을 props로 사용하면 좋다.
4. 컴포넌트 밖에서 handle 한다.
5. 컴포넌트 안에서 변경할 수 없다.
6. 값이 변경되지않고 사용자에게 보여지는 것은 props로 만드는 것이 좋다.
7. Static한 것도 props로 만들면 좋다

<mark>State</mark>

1. 컴포넌트 안에 있다.
2. 카운트 앱을 만들 때 state안에 변경되는 값을 저장할 수 있다.
3. 컴포넌트 안에서 handle 한다.
4. State를 변경하면 자동으로 업데이트 된다.
5. 값이 변경되어야 되는 건 state로 저장해야 된다.
6. 유저가 값을 업데이트하는 Form같은 것에 쓰면 좋다.

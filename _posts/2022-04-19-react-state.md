---
layout: post
title: React 'State' βοΈ
date: 2022-04-19 22:00 +0800
# last_modified_at: 2022-02-16 01:08:25 +0800
tags: [react]
toc: true
math: false
---

![React](https://ms314006.github.io/static/b7a8f321b0bbc07ca9b9d22a7a505ed5/97b31/React.jpg)

## π What is React 'State' ?

### State === μν

μΈκ°μκ²λ λ°°κ³ ν, μ λΉν¨, λ°°λΆλ¦ μ΄λΌλ μνκ° μ‘΄μ¬νλ€. μ¬λμ μ΄λ κ² 3κ°μ μνμ λ°λΌμ νλλ λ€λ₯΄κ² λλ€.

μ¦ <mark>κ³μν΄μ λ³ννλ νΉμ  μν, μνμ λ°λΌ κ°κ° λ€λ₯Έ λμμ ν¨</mark>

![Statebutton](https://cdn.dribbble.com/users/3482593/screenshots/6844698/switch.gif)

μμ μ¬μ§μ μμ¦ μ ννλ λ€ν¬νλ§μ΄λ€. μ΄κ²λ Dark μ΄κ±°λ Lightλ‘ ν΄λΌμ΄μΈνΈκ° μνλ₯Ό μ§μ  μ‘°μν  μ μκ² λ§λ  κΈ°λ₯μ΄λ€.

λ¦¬μ‘νΈμ μνλ μ»΄νΌλνΈκ° κ°λ νλ§μ²λΌ κ³μ κ°μ΄ λ°λ λμ μΈ λ°μ΄ν°μ΄κ³ , μνλ₯Ό λ°κΎΈλ λ±μ κ΄λ¦¬λ κ·Έ κΈ°λ₯μ κ°μ§ μ»΄νΌλνΈκ° μ§μ  κ΄λ¦¬νκ² λλ€.

κ·ΈλΌ μ΄μ  μμλ‘ μμλ³΄κ² λ€.

### μμ

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
        {/* μ΄λ κ² μμ±κ°μΌλ‘ propsλΌλ κ°μ μ λ¬ν  μλ μμ */}
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
  const [count, setCount] = useState(counterValue3); // props λ§€κ°λ³μλ‘ λ°μ νλ‘νΌν°λ‘ μ λ¬ λ°©λ²

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

μμ μ½λλ μ«μ λ°μ΄ν°μΈ countμ +μ -μ λ²νΌμΌλ‘ 1μ© λνκ±°λ λΉΌκ±°λ νλ κΈ°λ₯μ΄λ€.

κ°λ¨νμ§λ§ μ΄λ³΄λ€ λ μ’μ State μ¦ μνλ₯Ό λνλ΄λ μμλ μλ€. μ΄ countλ Counter componentμ νμ componentλ€μκ² PropsμΌλ‘ count κ°μ μ€ μλ μμΌλ©° μ΄ κ°μ κ° component λΌλ¦¬ μ κΈ°μ μΌλ‘ μνλ₯Ό κ³΅μ νκ² λλ€.

βοΈ λ€λ§!! μλ°μ€ν¬λ¦½νΈμμ λ³μλ₯Ό μ μΈν΄ λ°μ΄ν°λ₯Ό λ£κ³  κ³μ λ€λ₯Έ κ°μ λ£μ΄ μ¬μ©νλλΌλ©΄ λ¦¬μ‘νΈλ countμ μνλ₯Ό λ³κ²½νκΈ° μν΄μλ setCountλ‘λ§ μ κ·Όμ ν΄μΌνλ€. μλ°λ λ€λ₯Έ μΈμ΄λ€μ getter, setter μ κ°μ κΈ°λ₯μΌλ‘ λ³΄λ©΄ λ κ±° κ°λ€.

### π Propsμ Stateμ μ°¨μ΄

![ReactvsProps](https://res.cloudinary.com/practicaldev/image/fetch/s--xKWyj8SG--/c_imagga_scale,f_auto,fl_progressive,h_500,q_auto,w_1000/http://live-linguine-code.pantheonsite.io/wp-content/uploads/2019/03/react-state-vs-props.jpg)

<mark>Props(Properties)</mark>

1. Arguments of function
2. μ»΄ν¬λνΈ λ°μ μλ€.
3. μλ₯Ό μΉ΄μ΄νΈνλ μ±μ λ§λ λ€κ³  νμλ initial valueκ°μ κ²μ propsλ‘ μ¬μ©νλ©΄ μ’λ€.
4. μ»΄ν¬λνΈ λ°μμ handle νλ€.
5. μ»΄ν¬λνΈ μμμ λ³κ²½ν  μ μλ€.
6. κ°μ΄ λ³κ²½λμ§μκ³  μ¬μ©μμκ² λ³΄μ¬μ§λ κ²μ propsλ‘ λ§λλ κ²μ΄ μ’λ€.
7. Staticν κ²λ propsλ‘ λ§λ€λ©΄ μ’λ€

<mark>State</mark>

1. μ»΄ν¬λνΈ μμ μλ€.
2. μΉ΄μ΄νΈ μ±μ λ§λ€ λ stateμμ λ³κ²½λλ κ°μ μ μ₯ν  μ μλ€.
3. μ»΄ν¬λνΈ μμμ handle νλ€.
4. Stateλ₯Ό λ³κ²½νλ©΄ μλμΌλ‘ μλ°μ΄νΈ λλ€.
5. κ°μ΄ λ³κ²½λμ΄μΌ λλ κ±΄ stateλ‘ μ μ₯ν΄μΌ λλ€.
6. μ μ κ° κ°μ μλ°μ΄νΈνλ Formκ°μ κ²μ μ°λ©΄ μ’λ€.

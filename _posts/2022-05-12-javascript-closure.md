---
layout: post
title: Javascript 'Closure'
date: 2022-05-12 23:00 +0800
# last_modified_at: 2022-02-16 01:08:25 +0800
tags: [javascript]
toc: true
math: false
---

![Javascript](https://upload.wikimedia.org/wikipedia/commons/thumb/9/99/Unofficial_JavaScript_logo_2.svg/480px-Unofficial_JavaScript_logo_2.svg.png)

## What is Closure ? 💡

> 클로저는 함수와 함수가 선언된 어휘적 환경의 조합이다. by MDN

역시 MDN 말은 한번에 알아듣기 어려우므로 풀어서 정리해보자! 😅

클로져는 과연 무엇일까??

먼저 자바스크립트 Deepdive 책에 있는 에제로 보겠다.

```js
const outer = () => {
  const out = "outer!"; // 1. outer 함수 안에 지역변수 out 선언

  const inner = () => {
    console.log(out); // 2. 바깥의 out을 참조해 console.log 출력
  };

  return inner; // 3. 바깥의 out을 참조해 console.log를 출력하는 함수를 반환
};

const foo = outer(); // 4. outer함수 호출 -> 변수 foo에 inner함수의 주소값이 저장됨

foo(); // 5. 'outer!'
```

이 소스코드들은 클로져의 확실한 예시이다.

즉 클로져는 어떤 함수(outer) 내부에 선언된 함수(inner)가 바깥 함수(outer)의 지역변수(outerVariable)를 참조하는 것이 함수(outer)가 종료된 이후에도 계속 유지되는 현상을 말합니다. outer 함수의 라이프사이클이 inner 함수보다 짧을때 이야기이다.

⚠️ 다만 !! 전역컨텍스트에서 참조되는 outer 함수는 종료되는 것이 맞으나 사라지지않고 존재는 한다. 다만 메모리 어딘가에서 존재할뿐 가비지컬렉터에 의해서 완전히 소멸되는 것이 아니다. 적어도 inner 함수가 없어질 때까지는 outer 함수가 존재하게된다.

---

## Why Closure exist ? 🚨

### Scope

```js
function scopeA() {
  const a = "호랑이";

  function scopeB() {
    const a = "사자";

    console.log(a);
  }
  scopeB(); // 사자
  console.log(a);
}

scopeA(); // 호랑이
console.log(a); // reference error
```

scopeA를 호출 했을 때 사자가 아닌 호랑이가 출력되었다. 이것은 scopeB 함수의 변수 선언 및 할당 과정이 scopeA의 동작에 영향을 주지 않았다는 것이다. 즉, scopeA와 scopeB가 고유한 스코프를 가지고 있다고 말할 수 있습니다.

모든 프로그래밍 언어는 코드를 한 줄씩 읽는다. 그리고 이를 계산(앞으로는 평가한다고 하겠습니다.)해 메모리에 계산된 값을 저장(const a = '호랑이')하거나, 특정한 동작을(console.log(a))한다.

자바스크립트는 프로그램을 평가하기 전과 함수를 평가하기 전에 변수 선언과 함수 선언 정보를 미리 한 번 쭉 훑어서 수집한다. (실행컨텍스트의 Environment Record를 수집하는 과정)

프로그램을 시작하기 전에 scopeA함수 선언 정보를 수집하고 한 줄씩 평가를 하다가, scopeA가 호출되는 시점에 scopeA 내부의 (문자열 호랑이가 할당되는) a 와 scopeB의 정보를 수집하는 것이다. 이렇게 정보를 수집하고 다시 처음으로 돌아와 한 줄씩 평가를 시작하는데, 평가하는 코드줄에서 a에 값이 할당되거나, console.log(a)과 같이 사용될 때, 미리 수집해둔 정보를 가져와서 값을 새로 저장하고, 사용하는 것이다.

그렇기 때문에 함수 호출 전에 담긴 정보로는 다른 함수 내부의 변수를 알 수 있는 방법이 없다 그래서 각 함수는 고유한 스코프를 가지게 된다. (es6에서는 while, if, for문 같은 함수가 아닌 블록문에서도 새로 스코프를 만듦.) 이렇게 만들어진 스코프는 함수가 종료되면서 사라지게 된다.

### Scope Chain

스코프 내부에서 선언된 함수의 식별자는 알수 없지만 스코프 바깥의 식별자는 알 수 있다.

```js
function outer() {
  const outer = "outer!";

  function inner() {
    console.log(outer);
  }

  inner(); // outer!
}
```

자바스크립트는 스코프 내에 참조할 수 있는 변수나 함수가 존재하지 않으면 바깥의 스코프에서 식별자 정보를 찾는다.

이것이 가능한 이유는, 앞서 말했던 함수 평가 이전에 쭉 훑는 과정(변수 선언, 함수선언 수집) 이외에 바깥 스코프에 대한 정보를 수집하는 과정도 있기 때문이다. (실행컨텍스트의 outerEnvironmentReference에서 해당 실행컨텍스트의 렉시컬환경의 환경레코드를 참조하게된다.)

```js
function furtherOuter() {
  const furtherOuterVariable = "further outer!";

  function outer() {
    function inner() {
      console.log(furtherOuterVariable);
    }

    inner(); // further outer!
  }
}
```

자바스크립트 엔진은 스코프 안에 참조하는 식별자 정보가 없다면 함수 평가 전에 수집했던 바로 바깥 스코프로 가서 식별자를 찾는다. 바로 바깥 스코프에도 찾는 식별자가 없다면, 그 다음 스코프로 가서 찾고, 마지막엔 전역 스코프까지 가서 찾는데 이때도 존재하지 않는다면 참조에러 를 발생시킨다. 이렇게 스코프가 체인처럼 연결 되어있는 것을 스코프체인이라고 한다.

⚠️ 이때 주의해야할 것은 바로 바깥 스코프는 함수를 실행하는 시점의 바깥영역이 아닌 선언되는 시점의 바깥 스코프를 가리킨다. (렉시컬 스코프)

```js
function scopeA() {
  const a = "호랑이"; // 선언 시점의 상위 스코프

  function scopeB() {
    console.log(a);
  }

  return scopeB;
}

const scopeC = scopeA();

const a = "기린"; // 실행 시점의 상위 스코프(?)

scopeC(); // '호랑이'
```

---

## Closure 🚫

```js
const outer = () => {
  const out = "outer!"; // 1. 바깥 함수 outer의 스코프에 변수선언

  const inner = () => {
    console.log(out); // 2. 내부 함수 inner의 스코프에서 스코프체인을 타고 바깥 함수 스코프의 변수 참조
  };

  return inner; // 3. 1급 시민인 함수 inner를 바깥으로 반환
};

const foo = outer(); // 4.  foo에 inner함수의 주소값이 저장됨

foo(); // 5. outer함수 호출은 종료가 되어서 스코프가 사라져야 하지만 out은 여전히 잘 참조된다.
```

> 클로져는 어떤 함수(outer) 내부에 선언된 함수(inner)가 바깥 함수(outer)의 지역변수(outerVariable)를 참조하는 것이 함수(outer)가 종료된 이후에도 계속 유지되는 현상을 말한다.

💡 outer 함수 바깥으로 반환된 inner함수가 outer 함수의 outerVariable 변수를 참조하기에 메모리에 outer의 스코프가 여전히 남아있다.

### Closure 응용

1. 함수를 여러번 호출하면 상태가 연속적으로 유지될 때

```js
function outer() {
  let value = 0;

  return {
    increase() {
      ++value;
      console.log(value);
    },
    decrease() {
      --value;
      console.log(value);
    },
  };
}

const count = outer();
count.increase(); // 1
count.increase(); // 2
count.increase(); // 3
count.decrease(); // 2
count.decrease(); // 1
count.decrease(); // 0
console.log(value); // Error
```

위와 같이 함수를 호출하면 이전 함수 호출 상태가 기억되길 바랄 때 사용할 수 있다.

실제 사례로 프론트엔드 프레임워크인 React 의 hook API가 클로져를 통해서 구현되었다.

hook은 함수를 여러 번 호출하는 상황에서 데이터를 연속적으로 유지하는 기능이다.

```js
const Counter = () => {
  const [value, setValue] = useState(0); // 이 hook함수가 클로져를 통해 구현되었다.

  return (
    <div>
      <p>{value}</p>
      <button onClick={() => setValue(value + 1)}>+</button>
      <button onClick={() => setValue(value - 1)}>-</button>
    </div>
  );
};
```

상태value가 바뀌어 렌더링이 계속 일어남에 따라 Counter 함수가 여러 번 호출된다. 하지만 useState는 0이 아니라 이전 상태 value의 값을 유지하고 있다. 이는 useState 선언 시점의 바깥 변수에 0을 초기화한 다음, setValue로 해당 바깥 변수를 변경하는 것입니다. 다음 Counter가 호출되고 그 안의 useState가 다시 호출되면 변경된 바깥 변수를 value로 반환합니다.

2. 변수를 숨겨야 할 때

```js
let value = 0;

function increase() {
  console.log(++value);
}

function decrease() {
  console.log(--value);
}

function unknown() {
  value = -100000;
}

increase(); // 1
unknown(); // value: -100000
decrease(); // -100001
```

전역 변수로 선언해서 사실 위와 같은 클로져를 해결할 수 있는 방법이 있긴 있으나 만약 코드의 양이 많아지고 길어지게 된다면 어디서 해당 전역변수의 상태를 관리하는지 추적이 어려워지게 되고 가독성과 유지보수에 어려움을 겪게 한다.

```js
const counterCreator = () => {
  let value = 0;

  return {
    increase() {
      console.log(++value);
    },
    decrease() {
      console.log(--value);
    },
  };
};

const counter = counterCreator();

function unknown() {
  value = -100000;
}

counter.increase(); // 1
unknown(); // error: Uncaught ReferenceError: value is not defined
counter.decrease(); // 정상적으로 진행된다면 0
```

위와 같이 클로저로 함수를 만들면 외부에서 변수에 접근시 레퍼런스 에러가 발생하게 됩니다.

3. 함수가 독립적으로 동작해야할 때

카운터를 두 가지 독립적으로 해야하는 상황이 있다고 가정하자

```js
let myValue = 0;
let yourValue = 0;

function increaseMyCounter() {
  console.log(++myValue);
}

function decreaseMyCounter() {
  console.log(--myValue);
}

function increaseYourCounter() {
  console.log(++yourValue);
}

function decreaseYourCounter() {
  console.log(--yourValue);
}
```

이렇게 해버리면 코드가 너무 길어지고 지저분해 보인다.

그러면 클로져로 만들어보자

```js
const counterCreator = () => {
  let value = 0;

  return {
    increase() {
      console.log(++value);
    },
    decrease() {
      console.log(--value);
    },
  };
};

const myCounter = counterCreator();
const yourCounter = counterCreator();

myCounter.increase(); // 1
myCounter.increase(); // 2
yourCounter.increase(); // 1
myCounter.decrease(); // 1
```

위와 같이 myCounter와 yourCounter의 상태는 독립적이게 되었다.

🍔 클로저를 활용해 코드를 작성했기 때문에 가독성이 훨씬 좋아진 것을 볼 수 있다.

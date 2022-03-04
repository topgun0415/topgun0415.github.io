---
layout: post
title: Javascript Swallow Copy & Deep Copy (얕은 복사, 깊은 복사)
date: 2022-03-04 13:00 +0800
# last_modified_at: 2022-02-16 01:08:25 +0800
tags: [javascript]
toc: true
math: false
---

![Javascript](https://upload.wikimedia.org/wikipedia/commons/thumb/9/99/Unofficial_JavaScript_logo_2.svg/480px-Unofficial_JavaScript_logo_2.svg.png)

특히 데이터 타입이 다양하나 명확히 정해져있지 않은 자바스크립트에서는 데이터의 복사를 제대로 이해하고 있지 않으면 안될거 같아 이렇게 블로그로 기록하게 되었다. 자바스크립트에서는 3 가지의 복사 방법이 있다. 하지만 위에서 말한 3가지의 복사 방법을 알아보기 전에 미리 자바스크립트의 데이터를 정리해보자!

## 원시값과 참조값

- 원시 값 : 자바스크립트 내에서 사용할 수 있고, 필요한 '실제 값'을 갖는 어떠한 데이터이다. 자바스크립트에는 <mark>String, Number, Boolean, null, undefined</mark> 의 원시 값이 존재한다.

```javascript
let name = 'Philipuuu',
const nameCopy = name;
console.log(nameCopy); // Philipuuu
name = 'Himeru';
console.log(nameCopy); // Philipuuu
```

- 참조 값 : 자바스크립트에서 객체라고 불리는 것들의 주소를 참조하는 값이다. <mark>'Function', 'Array', 'Object', 'Regex'</mark> 등이 있다.

```javascript
const person = {
  name: "Philpuuu",
};
const personCopy = person;
console.log(personCopy.name); // Philipuuu
person.name = "Himeru";
console.log(personCopy.name); // Himeru
```

---

지금부터는 참조 위에서 말한 3가지 복사 방법에 대해서 알아보겠다.

## 1. 참조

```javascript
const a = [ name : 'Himeru' ];
const b = a;
a.name = 'Serin';
console.log(b.name) // Serin
```

변수 b에 a를 대입한 상황이다. a 변수의 name 속성값을 변경했는데, b 변수도 같이 변경된걸 볼 수 있다. 객체를 저장한 변수를 다른 변수에 대입하면 두 변수 모두 바뀌게 되는 것을 보게된다. 이러한 상황을 변수 a와 b가 같은 객체를 <mark>참조</mark>하고 있다고 한다. 이를 깊게 들어가면 매우 복잡해지므로 간단하게 설명하자면...

자바스크립트의 객체인 'Function', 'Array', 'Object', 'Regex'의 메모리 참조값을 말 그대로 참조한다는 의미이다. 이 객체들은 원시 데이터들보다 비교적 큰 공간을 차지해야 하므로 heap 이라는 공간에 어떠한 참조값(주소)을 가지고 저장되어진다.

---

## 2. 얕은 복사 (Swallow Copy)

<mark>얕은 복사</mark>는 중첩된 객체가 있을 때 가장 바깥 객체만 복사되고, 내부 객체는 참조 관계를 유지하는 복사를 의미한다.

```javascript
const arr = [{ name: "Philip" }, { age: 30 }];
const shallowCopy = { ...arr }; // 스프레드 문법으로 얕은복사 구현 가능 배열이면 [...] , 객체면 {...}
console.log(arr === shallowCopy); // false
console.log(arr[0] === shallowCopy[0]); // true
```

arr와 shallowCopy 변수는 서로 다른데 arr[0] === shallowCopy[0]의 결과값은 true 인것을 볼 수 있다. 이는 가장 바깥 객체는 복사되어 참조 관계가 끊어지므로 다른 값이 된다.

---

## 3. 깊은 복사 (Deep Copy)

<mark>깊은 복사</mark>를 하게되면 밖은 물론 안의 있는 객체들 참조값까지 달라지게 된다. <mark>깊은 복사</mark>를 그나마 따라한 것은 JSON.parse(JSON.stringify())를 쓰는 것이다.

```javascript
const arr = [{ name: "Philip" }, { age: 30 }];
const ref = arr; // 참조값을 받은 ref는 arr와 같은 참조값을 참조하게 된다.
const deepCopy = JSON.parse(JSON.stringify(arr)); // 깊은 복사
console.log(arr === ref); // true
console.log(arr[0] === ref[0]); // true
console.log(deepCopy === arr); // false
console.log(deepCopy[0] === arr[0]); // false
```

만약에 정말로 깊은 복사를 거진 완벽하게 하고 싶다면 <mark>npm install lodash</mark> 명령어를 통해 lodash 모듈을 설치한 뒤, lodash의 .cloneDeep() 함수를 사용해야 한다.

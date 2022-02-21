---
layout: post
title: Javascript Node traversing & walking (노드탐색) ✏️
date: 2022-02-21 18:00 +0800
# last_modified_at: 2022-02-16 01:08:25 +0800
tags: [javascript, dom]
toc: true
math: false
---

![Javascript](https://upload.wikimedia.org/wikipedia/commons/thumb/9/99/Unofficial_JavaScript_logo_2.svg/480px-Unofficial_JavaScript_logo_2.svg.png)

## 노드탐색 (Node walking)

자바스크립트로 DOM 조작 시 필수적으로 마주칠 수 밖에 없는 Node에 관해서 간단하게 복습하려 한다. <mark>바닐라 자바스크립트로 개인프로젝트를 하면서 DOM 트리 상에서 노드를 옮겨 다니며 부모, 형제, 자식 노드등을 탐색해야 할 일이 필수적으로 있을 것이다.</mark> To do list 를 만들면서 바닐라를 이용해 동적으로 노드를 만들어 해당 노드의 textContent를 얻으려 하였지만 게속해서 문제가 발생했다. 물론 ClassName나 ClassList를 추가하여 요소 노드를 취득하는 방법도 있겠지만 계속해서 부족했던 부모,형제,자식의 노드를 탐색하여 취득하는 연습도 해보고 싶었기에 찾아보게 되었고 간단하게 기록하였다.

### 부모 노드탐색(Parent Node)

부모 노드를 탐색하기 위해서는 `Node.prototype.parentNode`를 사용하여 취득한다.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <ul id="company">
      <li class="apple">apple</li>
      <li class="meta">meta</li>
      <li class="amazon">amazon</li>
    </ul>
  </body>
  <script>
    const $apple = document.querySelector(".apple");
    console.log($apple.parentNode); //<ul id='company'>...
  </script>
</html>
```

---

### 자식 노드탐색(Child Node)

자식 노드를 탐색하기 위해서는 다양한 프로퍼티들이 존재한다.

`Node.prototype.childNodes` : 자식 노드를 모두 탐색하여 담아 반환한다.

`Node.prototype.children` : 자식 노드 중에서 요소 노드만 모두 탐색하여 담아 반환함

`Node.prototype.firstChild` : 첫 번째 자식 노드를 반환함 (텍스트 노드, 요소 노드)

`Node.prototype.lastChild` : 마지막 자식 노드를 반환함 (텍스트 노드, 요소 노드)

`Node.prototype.firstElementChild` : 첫 번째 자식 노드를 반환함 (Only 요소 노드)

`Node.prototype.lastElementChild` : 마지막 자식 노드를 반환함 (Only 요소 노드)

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <ul id="company">
      <li class="apple">apple</li>
      <li class="meta">meta</li>
      <li class="amazon">amazon</li>
    </ul>
  </body>
  <script>
    const $company = document.querySelector("#company");

    console.log($company.childNodes); // NodeList(7) [text, li.apple, text, li.meta...]

    console.log($company.children); // [li.apple, li.meta, li.amazon]

    console.log($company.firstChild); // #text

    console.log($company.lastChild); // #text

    console.log($company.firstElementChild); // li.apple

    console.log($company.lastElementChild); // li.amazon
  </script>
</html>
```

---

### 형제 노드탐색(Sibling Node)

형제 노드를 탐색하기 위해서는 다양한 프로퍼티들이 존재한다.

`Node.prototype.previousSibling` : 부모 노드가 같은 형제 노드 중에서 자신의 이전 형제 노드를 탐색하여 반한함.

`Node.prototype.nextSibling` : 부모 노드가 같은 형제 노드 중에서 자신의 다음 형제 노드를 탐색하여 반한함.

`Node.prototype.previousElementSibling` : 부모 노드가 같은 형제 요소 노드 중에서 자신의 이전 형제 요소 노드를 탐색함

`Node.prototype.nextElementSibling` : 부모 노드가 같은 형제 요소 노드 중에서 자신의 다음 형제 요소 노드를 탐색함

---

### 노드 정보 취득

노드 객체에 대한 정보 취득을 하려면..

`Node.prototype.nodeType` : 노드 객체의 종류, 즉 노드 타입을 나타내는 상수를 반환함

`Node.prototype.nodeName` : 노드의 이름을 문자열로 반환

---

### 요소 노드의 텍스트 조작

`Node.prototype.nodeValue` : 해당 노드 객체의 값을 반환 및 변경

`Node.prototype.textContent` : 요소 노드의 텍스트와 모든 자손 노드의 텍스를 모두 취득하거나 변경

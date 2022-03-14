---
layout: post
title: Javascript Data Attribute & Dataset Property
date: 2022-03-14 13:00 +0800
# last_modified_at: 2022-03-14 01:08:25 +0800
tags: [javascript, dom]
toc: true
math: false
---

![Javascript](https://upload.wikimedia.org/wikipedia/commons/thumb/9/99/Unofficial_JavaScript_logo_2.svg/480px-Unofficial_JavaScript_logo_2.svg.png)

## Data Attribute 취득하기

Data Attribute & Dataset Property를 사용하면 HTML 요소의 정의한 사용자 정의 어트리뷰트와 자바스크립트 간에 데이터 교환이 가능하다.

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
    <ul class="fruit">
      <li id="1" data-fruit-id="1234" data-fruit-name="apple">apple</li>
      <li id="2" data-fruit-id="4567" data-fruit-name="grape">grape</li>
      <li id="3" data-fruit-id="7892" data-fruit-name="banana">banana</li>
    </ul>
  </body>
</html>
```

위와 같이 Data Attribute는 **data-fruits, data-role** 등 <mark>data 다음에 - 를 붙이고 개발자가 필요한 이름을 붙여서 사용한다.</mark>

Data Attribute의 값은 Dataset 프로퍼티로 취득할 수 있다. Data Attribute는 DOMStringMap이라는 객체를 반환한다.
그러므로 이를 자바스크립트에서 손쉽게 해당 Node를 불러올 수 있다.

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
    <ul class="fruit">
      <li id="1" data-fruit-id="1234" data-fruit-name="apple">apple</li>
      <li id="2" data-fruit-id="4567" data-fruit-name="grape">grape</li>
      <li id="3" data-fruit-id="7892" data-fruit-name="banana">banana</li>
    </ul>
    <script>
      const fruits = [...document.querySelector(".fruit").children];

      // fruit-Id가 '1234'인 요소 노드를 취득한다.
      const apple = fruits.find((fruit) => fruit.dataset.fruitId === "1234");
      // fruit-id가 '1234'인 요소노드에서 data-fruit-name 값을 취득
      console.log(apple.dataset.fruitName); //'apple'
      apple.dataset.fruitId = "4321";
      console.log(apple.dataset); // DOMStringMap {fruitId: '4321', fruitName:'apple'}
    </script>
  </body>
</html>
```

## Data Attribute 새롭게 추가하기

Data Attribute의 data- 이름 다음에 존재하지 않는 이름을 키로 사용하여 dataset 프로퍼티에 할당할 경우 새롭게 할당된다.

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
    <ul class="fruit">
      <li id="1" data-fruit-id="1234" data-fruit-name="apple">apple</li>
      <li id="2" data-fruit-id="4567" data-fruit-name="grape">grape</li>
      <li id="3" data-fruit-id="7892" data-fruit-name="banana">banana</li>
    </ul>
    <script>
      const fruits = [...document.querySelector(".fruit").children];

      // fruit-id가 '1234'인 요소 노드를 취득한다.
      const apple = fruits.find((fruit) => fruit.dataset.fruitId === "1234");

      // apple 요소 노드에 새로운 Data Attribute를 추가
      apple.dataset.price = "3$";
      console.log(apple.dataset);

      // DOMStringMap {fruitId: '4321', fruitName:'apple', price:'3$'}
    </script>
  </body>
</html>
```

이때 자바스크립트로 불러올 때는 개발자가 해당 캐밥케이스의 것을 캐멀케이스로 불러온 것과는 달리 dataset 프로퍼티에 추가한 카멜케이스의 프로퍼티 키는 Data Attribute의 data- 접두사 다음에 케밥케이스로 자동 변경되어 할당된다.

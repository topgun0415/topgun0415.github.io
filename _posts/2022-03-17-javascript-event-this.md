---
layout: post
title: Javascript Event This
date: 2022-03-17 13:00 +0800
# last_modified_at: 2022-03-16 01:08:25 +0800
tags: [javascript, dom]
toc: true
math: false
---

![Javascript](https://upload.wikimedia.org/wikipedia/commons/thumb/9/99/Unofficial_JavaScript_logo_2.svg/480px-Unofficial_JavaScript_logo_2.svg.png)

자바스크립트에는 다양한 <mark>This</mark>가 존재한다. 이벤트 핸들러 내부에도 <mark>This</mark>가 사용가능한데 한번 알아보자!

먼저 이벤트 핸들러 선언 방식은 3가지가 있다.

- 이벤트 핸들러 어트리뷰트 방식

```html
<button onclick="handleClick()">Click me</button>
```

- 이벤트 핸들러 프로퍼티 방식

```javascript
const $button = document.querySelector(".button");

$button.onclick = function (e) {};
```

- addEventListener 메서드 방식

```javascript
const $button = document.querySelector(".button");

$button.addEventListener("click", function (e) {});
```

---

## EventHandler Attribute 방식

이 예제에서의 <mark>This</mark>는 전역 객체 window / global 을 나타낸다

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>EventHandler This</title>
  </head>
  <body>
    <button onclick="handleClick()">Click me</button>
    <script>
      function handleClick() {
        console.log(this); // Global or Window
      }
    </script>
  </body>
</html>
```

이벤트 핸들러 어트리뷰트의 값으로 지정한 문자열은 사실 암묵적으로 생성되는 이벤트 핸들러의 문이라고 했다. 따라서 handleClick 함수는 이벤트 핸들러에 의해 일반 함수로 호출된다. 일반 함수로서 호출되는 함수 내부의 <mark>This</mark>는 전역 객체를 가리키므로 handleClick 함수 내부의 <mark>This</mark>는 전역 객체 window를 가리킨다.

다만 이벤트핸들러를 호출할 때 인수로 전달한 <mark>This</mark>는 이벤트를 바인딩한 DOM 요소를 가리킨다. 이는 이벤트 핸들러 프로퍼티 방식과 동일하다.

## EventHandler Property & addEventListener 메서드 방식

이벤트 핸들러 프로퍼티 방식과 addEventListener 메서드 방식 모두 **이벤트 핸들러 내부의 this는 이벤트를 바인딩한 DOM 요소**를 가리킨다. 즉 이벤트 핸들러 내부의 <mark>This</mark>는 이벤트 객체의 currentTarget 프로퍼티와 같다.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>EventHandler This</title>
  </head>
  <body>
    <button class="btn1">0</button>
    <button class="btn2">0</button>
    <script>
      const $button1 = document.querySelector(".btn1");
      const $button2 = document.querySelector(".btn2");

      // 이벤트 핸들러 프로퍼티 방식
      $button1.onclick = function (e) {
        console.log(this); // $button1
        console.log(e.currentTarget); // $button1
        console.log(this === e.currentTarget); //true

        // $button1의 textContext를 1 증가시킨다.
        ++this.textContent;
      };

      // addEventListener 메서드 방식
      $button2.addEventListener("click", function (e) {
        // this는 이벤트를 바인딩한 DOM 요소를 가리킨다.
        console.log(this); // $button2
        console.log(e.currentTarget); // $button2
        console.log(this === e.currentTarget); //true

        // $button2의 textContext를 1 증가시킨다.
        ++this.textContent;
      });
    </script>
  </body>
</html>
```

위 예제와는 다르게 화살표 함수로 정의한 이벤트 핸들러 내부의 <mark>This</mark>는 상위 스코프의 <mark>This</mark>를 가리킨다. 화살표 함수는 함수 자체의 <mark>This</mark>바인딩을 갖지 않기 때문이다.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>EventHandler This</title>
  </head>
  <body>
    <button class="btn1">0</button>
    <button class="btn2">0</button>
    <script>
      const $button1 = document.querySelector(".btn1");
      const $button2 = document.querySelector(".btn2");

      // 이벤트 핸들러 프로퍼티 방식
      $button1.onclick = (e) => {
        console.log(this); // window
        console.log(e.currentTarget); // $button1
        console.log(this === e.currentTarget); // false

        // this는 window를 가리키므로 window.textContent에 NaN(undefined + 1)을 할당
        ++this.textContent;
      };

      // addEventListener 메서드 방식
      $button2.addEventListener("click", (e) => {
        // this는 이벤트를 바인딩한 DOM 요소를 가리킨다.
        console.log(this); // window
        console.log(e.currentTarget); // $button2
        console.log(this === e.currentTarget); // false

        // this는 window를 가리키므로 window.textContent에 NaN(undefined + 1)을 할당
        ++this.textContent;
      });
    </script>
  </body>
</html>
```

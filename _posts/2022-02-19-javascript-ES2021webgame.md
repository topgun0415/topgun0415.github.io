---
layout: post
title: Let's get it 자바스크립트 프로그래밍 📚
date: 2022-02-19 10:00 +0800
# last_modified_at: 2022-02-16 01:08:25 +0800
tags: [javascript, book]
toc: false
math: true
---

![Let's get it 자바스크립트 프로그래밍](https://is4-ssl.mzstatic.com/image/thumb/Publication125/v4/30/79/e9/3079e96e-e9a9-9581-8612-4d5c815ea003/9791165215958.jpg/1200x630wz.png)

## 포기했던 책 다시 재도전 ..

프론트앤드계 네임드이신 [제로초](https://www.zerocho.com/)님! 😎 바로 이 책의 저자이다.

강의도 무료다! 강의는 여기서 👉 [ES2021 자바스크립트 강좌](https://www.youtube.com/watch?v=2yGhb-z8VTQ&list=PLcqDmjxt30RvEEN6eUCcSrrH-hKjCT4wt&index=1)

처음 자바스크립트를 시작할때 제로초님의 유툽 강의를 접하게 되었고 설명이 너무 좋아 빠져들게 되었다. 자바의 정석이 거진 끝날 무렵 이 책과 유툽 강의가 나오게 되어서 바로 구매하게 되었다.

책 초반에는 <mark>자바스크립트의 원시형 타입, 객체타입, if문, for문, 함수 선언 등의 기초문법</mark>을 배우고 2강부터는 자바스크립트로 DOM을 조작하여 웹게임을 만들어보는 그런 느낌이다. 작년 8월인가 9월에 이 책을 사서 시작하게 되었는데, 책 초반은 자바랑 크게 다르지 않아 빠르게 넘어갔다만.. 자바스크립트라는 언어를 너무 자바와 비슷하게 접근했던 것이 문제였다. 특히 초반 문법을 보면서 일급객체나 함수형 프로그래밍이라는 개념을 제대로 이해하지 못하고 넘어갔다 ㅋㅋ

첫 웹게임이 쿵쿵따인데 다행히도 HTML, CSS는 최소한으로 하고 최대한 자바스크립트 로직짜는거에만 집중해서 정말 만족했다. 그리고 무엇보다 만들어보면서 배우는거라 매우 재미를 느껴서 금방 금방 진도가 나갔다. 물론 중간에 Quiz나 보충설명도 나오고 매우 만족만족!

문제는 4강인가 5강에서부터 시작하였다 😭 자바를 잘하지는 못하지만 다른 프로그래밍 언어를 배웠던 것으로 버텼던게 자바스크립트 상에서 DOM API 관련 메서드들을 이해하지 못해서 코드 대부분이 이해가 가지 않았다.. 뿐만 아니라 실행컨텍스트와 스코프에 관해서 잘 모르니까 많이 헤맸다.. 결국에 7인강에서 코드를 보고 따라치는 수준으로 바뀌어버렸고 거기에서 의미를 못느껴서 잠시 접었었다.

이후 5개월이 지난 지금 모던 자바스크립트 Deep Dive 라는 책을 보았고, 그 사이 다양한 자바스크립트 강의들을 보면서 자바스크립트의 세계는 자바랑은 정말 전혀 다른 언어라는걸 느꼈다.. 자바와는 반대로 타입 제약이 없고 코드도 짧아 쓰기 입문하기에는 좋은 언어이나 사용하면 할 수록 어려운 언어라는걸 알았다 ㅋㅋㅋㅋ 이제는 이 책의 맨 마지막을 봐도 문법 적으로는 이해가 가능하며 할만해보인다고 느껴서 다시 도전하기로 마음 먹었다.

곧 3월 안으로는 리액트로 넘어가야하기 때문에 시간이 없으므로 이해가 잘 가지 않더라도 빠르게 넘어가보려 한다! 즉 이 책은 입문용으로는 살짝 어렵고, 어느정도 개인적으로 자바스크립트를 공부하고 시작해보길 바란다! 뒤에 웹게임 만드는거랑 추가적으로 웹게임에 이런저런 기능을 추가해보는 개인과제가 개인적으로 진짜 마음에 드는 컨텐츠 중에 하나이다 🤞

웹게임은 <mark>쿵쿵따, 계산기, 숫자야구 게임, 로또 추첨기, 가위바위보, 반응속도 테스트, 틱택토 게임, 텍스트 RPG, 카드 짝 맞추기, 지뢰 찾기, 2048게임, 두더지 잡기</mark>가 있다!

쿵쿵따 예시 코드다.

```javascript
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>word-relay</title>
  </head>
  <body style="box-sizing: border-box; margin: 0">
    <h1>This is word-relay game</h1>
    <div style="font-weight: bold; color: coral; font-size: 50px">
      <span id="order">1</span> player
    </div>

    <!-- word showing box -->
    <div
      style="
        width: 200px;
        height: 20px;
        border-radius: 5px;
        border: 3px solid dodgerblue;
        background-color: dodgerblue;
        color: white;
        text-align: center;
        padding: 25px;
      "
    >
      <span id="word" style="font-weight: bolder; font-size: 20px"
        >word showing box</span
      >
    </div>
    <br />
    <!-- word input box -->
    <input type="text" />
    <!-- input btn  -->
    <button>Button</button>
    <script>
      // Selectors
      const $order = document.querySelector('#order');
      const $word = document.querySelector('#word');
      const $btn = document.querySelector('button');
      const $input = document.querySelector('input');

      // Variable
      let word; // 제시어
      let newWord; // 입력어

      // Greeting
      const players = Number(prompt('How many person do you want to play?'));
      alert(`There are ${players} players `);
      confirm('Are you sure?');

      // Event function
      $input.addEventListener('input', (e) => {
        wordLower = e.target.value;
        newWord = wordLower.toLowerCase();
      });

      $btn.addEventListener('click', (e) => {
        // word-relay
        if (!word) {
          // 제시어가 비어있는 경우
          word = newWord;
          $word.textContent = word;
          $input.value = '';
          console.log(word[word.length - 1]);
        } else {
          // 제시어가 비어있지 않은 경우
          if (word[word.length - 1] !== newWord[0]) {
            alert('Please write your word again');
          } else {
            word = newWord;
            $word.textContent = word;
            $input.value = '';
          }
        }

        // add player number
        if (parseInt($order.innerText) === players) {
          $order.innerText = 1;
        } else {
          ++$order.innerText;
        }

        $input.focus();
      });
    </script>
  </body>
</html>
```

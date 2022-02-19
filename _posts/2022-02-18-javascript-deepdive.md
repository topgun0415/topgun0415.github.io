---
layout: post
title: 모던 자바스크립트 Deep Dive 📚
date: 2022-02-18 01:00 +0800
# last_modified_at: 2022-02-16 01:08:25 +0800
tags: [javascript, book]
toc: true
math: true
---

![deep-dive](https://media.vlpt.us/images/hustle-dev/post/9a376a17-0fb6-4689-9553-4e454ce1b3ca/%E1%84%86%E1%85%A9%E1%84%83%E1%85%A5%E1%86%AB%20%E1%84%8C%E1%85%A1%E1%84%87%E1%85%A1%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%B8%E1%84%90%E1%85%B3.png)

# 드디어 1회독 완료..

이런저런 사정이 있어서 책을 한번 다 읽는데 오랜시간이 걸렸지만 첫 사이클을 꼼꼼하게 읽는 타입이라 더 오래걸린 것도 없지않아 있는것 같다. 😅

<mark>자바의정석</mark>이란 책으로 프로그래밍 세게에 입문한 나는 스프링으로 갈지 자바스크립트로 갈지 정말 오래 고민했던것 같다. 하지만 프론트앤드로 근무하던 대학 동기의 설득에 자바스크립트를 처음 접하게 되었고 크게 멘붕이 왔었다 🥲 뭐 이런 근본없고 어려운 언어가 다있지? 라는 생각으로 접을려던 시점에 유튜브에서 자바스크립트 매력에 대해서 설명하는 영상을 보게 되었고 금새 프론트앤드가 되고싶다고 결정했던것 같다.

첫 자바스크립트 책으로 제로초님의 <mark>Let's get it 자바스크립트</mark>라는 책을 구매하여 보았고, 노마드코더님의 자바스크립트 강의 등등 몇 개 더 보았지만 이해하기가 너무 어려웠을뿐더러 자바스크립트의 세계관이 생각외로 엄청 깊고 방대하다는 것을 알게되엇다. 좀 더 딥하게 자바스크립트를 공부해보고 싶은 나는 바로 구글링을 하기 시작했고 결국 자바스크립트의 정석이라는 이 자바스크립트 딥다이브라는 책을 알게 되었다.

자바스크립트의 기본적인 문법만 보고 자바스크립트의 프레임워크인 React나 Vue 그리고 Angular로 넘어가게된다면 분명 어렵고 이해도 안될뿐더러 계속해서 나오는 개념들을 외우기만 하게 될 것이다... 이건 순수하게 나의 경험담이므로 이 글을 읽는 다른분들은 어떨지는 모르겠다! 다만 프론트앤드의 기초중에 기초이며 가장 중요한 Javascript에 시간을 들여 깊게 공부할 만한 충분한 가치가 있다고 생각한다. 다만 살짝 아쉬운건 실습이나 과제가 없으므로 [모던 자바스크립트 튜토리얼](https://ko.javascript.info/)에 들어가서 과제도 같이 풀어보면 훨씬 잘 이해가 갈 것이다

앞으로 꾸준하게 이 책을 3개월 한번씩 회독을 진행해나갈 예정이며, 자바스크립트로 프로젝트를 하다가 모르는 개념이 나오면 지속해서 참고해나갈것이다. 밑에는 책의 목차들을 나열해보았으니 참고해보면 좋을것 같다~! 😃

## 모던 자바스크립트 딥다이브 목차 🗂️

▣ 01장: 프로그래밍

▣ 02장: 자바스크립트란?

▣ 03장: 자바스크립트 개발 환경과 실행 방법

▣ 04장: 변수

▣ 05장: 표현식과 문

▣ 06장: 데이터 타입

▣ 07장: 연산자

▣ 08장: 제어문

▣ 09장: 타입 변환과 단축 평가

▣ 10장: 객체 리터럴

▣ 11장: 원시 값과 객체의 비교

▣ 12장: 함수

▣ 13장: 스코프

▣ 14장: 전역 변수의 문제점

▣ 15장: let, const 키워드와 블록 레벨 스코프

▣ 16장: 프로퍼티 어트리뷰트

▣ 17장: 생성자 함수에 의한 객체 생성

▣ 18장: 함수와 일급 객체

▣ 19장: 프로토타입

▣ 20장: strict mode

▣ 21장: 빌트인 객체

▣ 22장: this

▣ 23장: 실행 컨텍스트

▣ 24장: 클로저

▣ 25장: 클래스

▣ 26장: ES6 함수의 추가 기능

▣ 27장: 배열

▣ 28장: Number

▣ 29장: Math

▣ 30장: Date

▣ 31장: RegExp

▣ 32장: String

▣ 33장: 7번째 데이터 타입 Symbol

▣ 34장: 이터러블

▣ 35장: 스프레드 문법

▣ 36장: 디스트럭처링 할당

▣ 37장: Set과 Map

▣ 38장: 브라우저의 렌더링 과정

▣ 39장: DOM

▣ 40장: 이벤트

▣ 41장: 타이머

▣ 42장: 비동기 프로그래밍

▣ 43장: Ajax

▣ 44장: REST API

▣ 45장: 프로미스

▣ 46장: 제너레이터와 async/await

▣ 47장: 에러 처리

▣ 48장: 모듈

▣ 49장: Babel과 Webpack을 이용한 ES6+/ES.NEXT 개발 환경 구축
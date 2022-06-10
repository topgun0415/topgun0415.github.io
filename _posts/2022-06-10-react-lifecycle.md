---
layout: post
title: React LifeCycle ⚛️
date: 2022-06-10 22:00 +0800
# last_modified_at: 2022-02-16 01:08:25 +0800
tags: [react]
toc: true
math: false
---

![React](https://ms314006.github.io/static/b7a8f321b0bbc07ca9b9d22a7a505ed5/97b31/React.jpg)

## 🧬 What is LifeCycle in React ?

한국어로는 <mark>생명주기</mark>라 부른다.

리액트에서 컴포넌트가 나타날때, 업데이트될 때, 사라질 때 중간중간 어떠한 작업들을 실행시키고 싶을때 사용하는 것이 이 LifeCycle API를 사용하면 된다.

![LifeCycle](https://cdn.filestackcontent.com/ApNH7030SAG1wAycdj3H)

사진에서 보이듯이 다양한 API들이 존재하기 때문에 매우 복잡하고 어려워보이지만 사실 외울 필요는 없고 개념을 이해하고 나중에 쓸 때 사용하면 된다. 하지만 이는 현재 Hook을 사용하는 함수형 컴포넌트에서 사용하지 않기 때문에 사용할 일은 크게 없겠지만 그래도 레거시 클래스 컴포넌트 코드를 보고 이해할 필요가 있기 때문에 꼭 알아두는 것이 좋다.

---

## 🥚 Mounting

컴포넌트가 우리 브라우저 상에 나타난다는 의미

### Constructor

컴포넌트가 가지고 있을 State 초기설정을 한다던지 아니면 컴포넌트가 만들어질때 해야하는 초기의 작업들이 있을때 설정한다.

### getDerivedStateFromProps

Props로 받은 값을 State에 동결시키고 싶을 때 사용하는 API이다. 마운팅 과정에서도 있고, 업데이트 과정에서도 Props가 바뀌게 되면 실행된다.

### Render

우리가 어떤 돔을 만들게 될지, 태그들의 어떤 값을 전달할건지 정의해주게 된다.

### componentDidMount

랜더함수가 실행되고 브라우저 상에 컴포넌트가 나타나게 된다면 componentDidMount가 실행된다. 이 API에서는 외부 라이브러리를 사용할 경우 여기서 사용할 수 있으며, 네트워크 AJAX 요청을 할 때도 이 API에서 사용하게 된다. 또한 컴포넌트가 나타나고 몇 초 뒤에 실행하고 싶은 작업도 할 수 있다.

---

## 🐓 Updating

부모 컴포넌트나 State & Props 가 바뀌어서 재랜더링 되는 것을

### shouldComponentUpdate

컴포넌트가 업데이트 되는 성능을 최적화 시킬때 사용된다. 리액트에서는 부모 컴퍼넌트가 리랜더링 되면 자식 컴포넌트 render 함수도 다 실행되게 된다. 하지만 이 작업들이 불편할 수 도 있다. 리액트에서는 리랜더링이 발생하게 된다면 가상 돔에 그려 실제 돔과 비교하여 생긴 차이를 실제 돔에 리랜더링 하는 방식으로 작동되는데, 만약에 가상 돔에 몇 천개의 컴포넌트들이 그려진다고 하면 그것도 성능상으로 저하로 이어질 수 있기 때문에 성능 최적화를 위해서는 매우 중요한 API이다. 이 API는 true / false 값을 리턴하고 true로 반환하게 된다면 render 함수가 실행된다. 즉 Virtual DOM에도 랜더링을 할지 말지 결정하는 함수라고 생각하면 된다.

### getSnapshotBeforeUpdate

이는 랜더링하고 바로 랜더링의 결과물이 브라우저상에 반영되기 바로 직전에 호출되는 함수이다.

### componentDidUpdate

Updating 작업을 마치고 컴포넌트가 업데이트 되었을 때 호출되는 함수이다.

---

## 🪦 UnMounting

컴포넌트가 우리 브라우저 상에서 사라질 때

그러면 위에 있는 사진의 각 API들을 하나씩 알아보자

### componentWillUnmount

언마운팅 과정에서 컴포넌트가 브라우저에서 사라질 때 호출되는 함수이다.

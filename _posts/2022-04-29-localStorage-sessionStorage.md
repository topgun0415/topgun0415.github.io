---
layout: post
title: LocalStorage & SessionStorage 💾
date: 2022-04-29 20:00 +0800
# last_modified_at: 2022-02-16 01:08:25 +0800
tags: [web]
toc: true
math: false
---

![WebStorage](https://edteam-media.s3.amazonaws.com/blogs/original/e20cb48d-1d63-407f-9352-ce41c24eec98.png)

기본적으로 Storage는 Cookie와 유사하지만 더 안정적이고 웹 브라우저에 특정 저장공간이라고 이해하면 된다.

LocalStorage와 SessionStorage는 동일하나 쓰임새는 구분할 줄 알아야한다.

## 💿 LocalStorage ?

🔻 로컬스토리지는 아래와 같은 특성이 있다

1. 만약 PC에 저장하면 PC에 남아있고. 태블릿에 저장하면 태블릿에 남아있는 특징이 있다. 그러므로 각 접속하는 기계에 따라 보여지는 것이 다를 수 있다.

2. 도메인 별로 따로 저장되게 된다.

3. 삭제하기 전까지는 남아있다.

각기 다른 html 파일을 열어 실행하여도 로컬스토리지를 공유할 수 있기 때문에 로그인 정보라든지 어떤 특정 지워지지않아야 할 값들을 보존할 수 있기에 매우 유용하다.

▶️ 추가

```
localStorage.setItem('key', 'value')
```

▶️ 확인

```
localStorage.getItem('key')
```

❗️ 저장했던 데이터의 value값을 조회할 수 있게 된다

▶️ 제거

```
localStorage.removeItem('key');
```

▶️ 전부 제거

```
localStorage.clear();
```

---

## 📀 SessionStorage ?

LocalStorage는 일부로 지워주지 않는 이상 게속 그 정보가 남아있게 된다. 사용자 입장에서는 일일이 지워야하기 때문에 매우 불편하다.

즉 단발성 데이터들은 SessionStorage 저정하자!

1. 해당 브라우저 창이 꺼지면 즉 페이지 세션이 끝날 때, 이와 함께 데이터는 날라가게 된다.

▶️ 추가

```
sessionStorage.setItem('key', 'value')
```

▶️ 확인

```
sessionStorage.getItem('key')
```

❗️ 저장했던 데이터의 value값을 조회할 수 있게 된다

▶️ 제거

```
sessionStorage.removeItem('key');
```

▶️ 전부 제거

```
sessionStorage.clear();
```

---

## ⛔️ 주의해야 할 점

우선 이 Storage들은 기본적으로 문자열만 저장 가능하다는 점이 있다. 이러한 이유는 데이터베이스들의 저장방식은 <mark>JSON 타입의 저장 방식</mark>을 따르기 때문이다.

예를 들어 localStorage나 SessionStorage의 저장 value들은 무조건 <mark>String Type</mark>이어야 한다.

```
localStorage.setItem('Cake', '1');
sessionStorage.setItem('Cake', '3');
```

또한 객체도 String을 만들어줘야 하는 건 마찬가지이다.

```js
const arr = [1, 2, 3];
const person = {
  name: "philip",
  age: 30,
};

localStorage.setItem("arr", JSON.stringify(arr));
localStorage.setItem("person", JSON.stringify(person));
```

이렇게 저장을 해줘야지 객체가 잘 저장된다.

⚠️ 만에 하나 객체를 그 상태로 바로 집어넣게 되면 Storage에서는 Obj 라는 형태로 저장되게 된다.

# 정리하자면 ...

각종 에디터에서 만든 값들을 JSON 형태로 만들어 Web Storage나 Database 저장하고 싶다 ?

🅰️ JSON.stringify()

반대로 Web Stroage 혹은 Database에 저장되어 있는 값을 내가 에디터에서 불러와 쓸 수 있는 데이터로 변환 시키고 싶다?

🅱️ JSON.parse()

왜냐하면 Web Storage나 Database는 모두 JSON 형태의 저장방식을 고수하고 있기 때문이다.

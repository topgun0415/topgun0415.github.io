---
layout: post
title: React SPA & CSR ⚛️
date: 2022-04-23 14:00 +0800
# last_modified_at: 2022-02-16 01:08:25 +0800
tags: [react]
toc: true
math: false
---

![React](https://ms314006.github.io/static/b7a8f321b0bbc07ca9b9d22a7a505ed5/97b31/React.jpg)

## 📡 라우팅이란 무엇일까 ?

<mark>어떤 네트워크 내에서 통신 데이터를 보낼 경로를 선택하는 일련의 과정</mark>

ROUTER : 데이터의 경로를 실시간으로 지정해주는 역할을 하는 무언가

ROUTING : 경로를 정해주는 행위 자체와 그런 과정들을 다 포함하여 일컫는 말

![Routing](https://www.sangoma.com/wp-content/uploads/how-ip-routing-works-diagram-1.png)

## 🌀 PAGE ROUTING

![Standard](https://mobidev.biz/wp-content/uploads/2021/07/3-tier-web-architecture.jpg)

기본적으로 클라이언트는 어떤 사이트에 들어가게 되면 그 사이트의 웹서버로 html파일을 요청을 하게 되고, 그 요청을 받은 웹서버는 요청받은 클라이언트로 파일들을 뿌려주게 된다.

### MPA (Multipage Application)

![MPA](https://mobidev.biz/wp-content/uploads/2021/07/ssr-web-app-architecture-diagram-1.jpg)

멀티페이지 어플리케이션이란 웹서버가 각기 다른 page들의 html 파일들을 가지고 있다가 클라이언트가 해당 페이지에 GET 요청을 하면 그것을 인식하고 html 파일을 뿌려주는 역할을 하는데 브라우저는 응답을 받으면 <mark>화면이 깜빡거림과 동시에 이를 랜더링 하여 보여주게 된다</mark>

### SPA (Singlepage Application)

![SPA](https://mobidev.biz/wp-content/uploads/2021/07/spa-web-app-architecture-diagram.jpg)

멀티페이지 어플리케이션과는 반대로 웹서버가 말 그대로 단 한가지의 페이지만 가지고 요청에 따라 index.html만 뿌려주는 역할을 하게된다. 만약에 클라이언트가 페이지를 이동하고 싶다고 해도 페이지가 하나밖에 없기 때문에 지속해서 index.html만 뿌려주게 된다.

예를 들어 혹시나 내가 어떤 사이트에서 페이지 이동을 하려고 버튼을 눌렀다고 치자. 그럼 클라이언트는 자동으로 GET 혹은 POST로 해당 리소스를 요청하게 된다. 근데 원래 같았으면 웹 서버가 이 HTTP 메서드 요청을 받아서 데이터베이스에 있는 해당 요청 html을 찾아서 가져다 주는 것이지만 SPA 방식은 클라이언트 요청이 바로 REACT APP이 자동으로 알아서 페이지를 업데이트 시켜버린다 (컴포넌트를 교체).

이런 방식으로 페이지를 이동하게 되면 페이지를 이동할때마다 웹서버를 통해 기다리는 시간 자체가 사라져버리기 때문에 사용자 입장에서는 누르는 즉시 페이지가 바뀌는 것을 경험하게 되고, 이건 마치 휴대폰에서 앱의 반응속도를 똑같이 경험할 수 있게 된다. 혹시나 각각 페이지에 실시간으로 받아오는 데이터가 필요할 경우에는 웹서버와 데이터만 요청하고 전달 받게 된다. 혹시나 시간이 걸리는 규모의 데이터라고 해도 로딩페이지를 띄워놓고 뷰라도 먼저 보이게끔 하는 방법도 있다.

이런 방식은 클라이언트 측에서 알아서 랜더링을 한다고 해서 <mark>CSR (Client Side Rendering)</mark>이라고 부른다.

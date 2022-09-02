---
layout: post
title: Apache 🪶 & Tomcat 🐈
date: 2022-09-02 20:00 +0800
# last_modified_at: 2022-02-16 01:08:25 +0800
tags: [web, java]
toc: true
math: false
---

<br />

우리가 흔히 사용하는 웹페이지는 아파치와 톰캣으로 이루어져 있다고 할 수 있다. 특히나 linux를 공부하다보면 Apache Tomcat을 설치해야한다. 그럼 대체 아파치는 무엇이고 톰캣은 무엇일까?

## Apache 🪶

![Apache](https://takabus.com/tips/wp-content/uploads/2021/10/apache%E3%83%AD%E3%82%B4.png)

아파치 소프트웨어 재단의 오픈소스이다. <mark>웹서버</mark>라고 불리고 클라이언트의 HTTP 요청이 왔을시에만 응답하는 정적 웹페이지에 사용한다.

- 80번 포트로 클라이언트 요청(POST, GET, DELETE)에만 응답
- HTML, CSS, 이미지와 같은 유저와 상호작용하지 않은 정적인 데이터만 처리

---

## Tomcat 🐈

![Tomcat](https://images.velog.io/images/always/post/9099162c-cc77-4517-a229-f142264351f0/2a8a70178a41a70713786f4f5f8f6c9a.jpeg)

아파치와는 반대로 WAS(Web Application Server)이며 동적인 웹을 만들기 위한 <mark>웹 컨테이너</mark>이다.<mark>서블릿 컨테이너</mark>라고도 불린다. 😺

JSP, ASP, PHP 등은 웹 컨테이너인 톰캣에게 전달한다.

- 컨테이너, 웹 컨테이너, 서블릿 컨테이너라고 부름
- JSP, 서블릿처리, HTTP 요청 수신 및 응답

톰캣을 쓰면 동적인 데이터가 처리함이 가능해짐. DB연결, 데이터 조작, 다른 운용프로그램과 상호 작용이 가능하다. MVC 모델 2를 가능하게 만들어 주는 고양이다.

---

## Apache Tomcat 🪶🐈

![Tomcat](https://images.velog.io/images/g00dluckroon/post/b1ad3810-5b1f-40cc-aa18-bec30f2eca62/%ED%86%B0%EC%BA%A3.PNG)

이번에는 아파치 톰캣이란 녀석이다! 고양이에게 날개를 달아 주었다! 그만큼 더 할 수 있는 것들이 많아졌다고 생각하면 쉽다.

이 아파치 톰캣도 물론 WAS(Web Application Server)이다.

아파치만 사용하게 된다면 사실 정적인 웹페이지밖에 처리 못하는데 반해 그렇다고 톰캣만 사용하여 동적인 웹페이지를 처리한다고 하면 과부하가 올 수 있다. 물론 얼마 되지 않은 클라이언트의 요청이라면 여유롭게 받아칠 수 있겠지만.. 아무리 큰 가게에 짬이 있는 알바생이 있다고 한들 손님이 많아져버리면 모든 주문에 빨리 대응할 수 없는 것 처럼 말이다 😹

그렇기에 아파치 톰캣을 통해 정적인 페이지와 동적인 페이지를 분산처리 하여 과부하를 막을 수 있다. 🔧

밑에 있는 사진들을 참고하자!

## Web Server & Web Application Server

![WAS](https://camo.githubusercontent.com/5ba9c98e29a385a593c1f86546a00dd69b6f977f/68747470733a2f2f676d6c776a64393430352e6769746875622e696f2f696d616765732f7765622f7374617469632d76732d64796e616d69632e706e67)

![WAS](https://camo.githubusercontent.com/4fa9ee213bd779b35eaad55fe4fa3eefc5ddf9f5/68747470733a2f2f676d6c776a64393430352e6769746875622e696f2f696d616765732f7765622f7765627365727665722d76732d776173312e706e67)

## Web Server Architecture

다른 포스팅에서 다시 다루겠지만 서블릿을 포함한 MVC 모델이 그림에서 쉽게 설명해주고 있으므로 꼭 참고하도록 하자!

![WAS](https://camo.githubusercontent.com/adc4d173996d5db6bf1bae0b5be952b3a4e23e7a/68747470733a2f2f676d6c776a64393430352e6769746875622e696f2f696d616765732f7765622f7765622d736572766963652d6172636869746563747572652e706e67)

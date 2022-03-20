---
layout: post
title: 모든 개발자를 위한 HTTP 기본지식 2편 🌎
date: 2022-03-20 18:00 +0800
# last_modified_at: 2022-02-16 01:08:25 +0800
tags: [http]
toc: true
math: false
---

![lecture](https://cdn.inflearn.com/public/courses/326277/cover/52d4f143-b470-4109-96cb-a0b146fb42ed/http.png)

## ⭐ URI와 웹 브라우저 요청 흐름

### URI (Uniform Resource Identifier )

![URI](https://i0.wp.com/hanamon.kr/wp-content/uploads/2021/09/URL-URN.jpeg?resize=547%2C181&ssl=1)

URL : Resource Location
URN : Resource Name

URI 단어 뜻

- Uniform : 리소스 식별하는 통일된 방식
- Resource : 자원, URI로 식별할 수 있는 모든 것(제한 없음)
- Identifier : 다른 항목과 구분하는데 필요한 정보

URL 전체문법

https://www.google.com:443/search?q=hello&hl=ko

- Scheme

- Protocol(https)

- Port(443)

- Path(/search)

- Query Parameter(q=hello&hl=ko)

---

### 웹 브라우저 요청 흐름

https://www.google.com:443/search?q-hello&hl=ko

1. DNS 조회 / IP 조회 /
2. HTTP 요청 메시지를 보냄
   <br> <mark>웹 브라우저가 HTTP 메시지 생성</mark> -> <mark>SOCKET 라이브러리를 통해 전달 (TCP/IP 연결 & 데이터전달)</mark> -> <mark>TCP/IP 패킷 생성, HTTP 메시지 포함</mark> -> <mark>LAN 드라이버 & LAN 장비를 통해서 물리적 네트워크 인터페이스를 통해 인터넷으로 흘러들어가게 되고 이는 서버로 보내지게 된다.</mark>

3. 웹 서버에서 HTTP 응답 메시지 만듦 (다시 TCP/IP로 포장한다)
4. 웹 브라우저 HTML Randering

---

## ⭐ HTTP 기본

### 모든 것이 HTTP

<mark>HyperText Transfer Protocol</mark>

- HTML, TEXT
- IMAGE, 음성, 영상, 파일
- JSON, XML
- 거의 모든 형태의 데이터 전송 가능
- 서버간에 데이터를 주고 받을 때도 대부분 HTTP 사용

<h1> 지금은 HTTP 시대! </h1>

HTTP 역사는 두 가지만 기억하자!

- <mark>HTTP/1.1 1997년 : 가장 많이 사용, 우리에게 가장 중요한 버전</mark>
- HTTP/2.0 2015년 : 성능 개선
- HTTP/3 진행중 : TCP 대신에 UDP 사용, 성능 개선

기반 프로토콜

- TCP : HTTP/1.1, HTTP/2 (주로 사용중)
- UDP : HTTP/3 (점점 증가중)

---

### 클라이언트 서버 구조

- Request Response 구조

- 클라이언트는 서버에 요청을 보내고, 응답을 대기

- 서버가 요청에 대한 결과를 만들어서 응답

클라이언트와 서버간의 요청 & 응답 통신방법이 단순하지만 매우 중요하다.
이는 클라이언트단은 화면이나 어떠한 기능에만 신경 쓸 수 있어서 효과적으로 일 할 수 있을뿐더러, 서버단도 어떻게 효율이 좋은 서버를 만드는지 아키텍쳐를 짜는데 더 많은 시간을 쓸 수 있기 때문이다. 즉 양쪽이 독립적으로 일을 할 수 있다는 것이 큰 장점!

---

### 무상태 프로토콜 (Stateless) 지향

- 서버가 클라이언트의 상태를 보존 ❌
- 장점 : 서버 확장성 높음 (스케일 아웃)
- 단점 : 클라이언트가 추가 데이터 전송

Stateful과 Stateless 차이점을 잘 알아볼 것!

상태유지 : 중간에 다른 점원으로 바뀌면 안된다.
(중간에 다른 점원으로 바뀔 때 상태 정보를 다른 점원에게 미리 알려줘야 한다.)

무상태 : 중간에 다른 점원으로 바뀌어도 된다.

- 갑자기 고객이 증가해도 점원을 대거 투입할 수 있다.
- 갑자기 클라이언트 요청이 증가해도 서버를 대거 투입할 수 있다.

🚫 Stateless 실무 한계

- 모든 것을 무상태로 설계 할 수 있는 경우도 있고 없는 경우도 있다.
- 무상태 : 로그인 필요 없는 단순한 서비스 소개화면
- 상태유지 : 로그인
- 로그인한 사용자의 경우 로그인 했다는 상태를 서버에 유지
- 일반적으로 브라우저 쿠키와 서버 세션등을 사용해서 상태 유지
- 상태유지는 최소한만 사용

---

### 비연결성 (connectionless)

연결을 유지하는 모델 : 서버는 연결을 게속 유지하기 때문에 서버 자원을 지속해서 소모

연결을 유지하지 않는 모델 : 서버는 연결 유지를 하지 않기 때문에 최소한의 자원 유지

- HTTP는 기본이 연결을 유지하지 않는 모델

- 일반적으로 초 단위의 이하의 빠른 속도로 응답

- 1시간 동안 수천명이 서비스를 사용해도 실제 서버에서 동시에 처리하는 요청은 수십개 이하로 매우 작음 (예 : 웹 브라우저에서 계속 연속해서 검색 버튼을 누르지 않기 때문에)

- 서버 자원을 매우 효율적으로 사용할 수 있음

🚫 비연결성의 한계와 극복

- TCP/IP 연결을 새로 맺어야함 - 3way handshake 시간 추가
- 웹 브라우저로 사이트를 요청하면 HTML 뿐만 아니라 자바스크립트, css도 추가해서 다운로드 됨
- 지금은 HTTP 지속연결로 문제 해결
- HTTP/2, HTTP/3에서 더 많은 최적화

<h1>스테이스리스를 기억하자!</h1>
서버 개발자들이 어려워하는 업무

- 정말 같은 시간에 딱 맞추어 발생하는 수 만 건의 대용량 트래픽 (예 : 치킨 이벤트, 선착순 이벤트, 명절 KTX 예약)

---

### HTTP 메시지 ✉️

HTTP 요청 메시지와 응답 메시지는 다르다.

![HTTPmessage](https://media.vlpt.us/post-images/codemcd/f03c8e00-e267-11e9-a634-d9d33e59b626/HTTP3-7.png)

<mark>요청 메시지 : GET /search?q=hello&hl=ko HTTP/1.1</mark>
시작 라인 : 요청 메시지(HTTP 메서드), 요청 대상, HTTP 버전

- 종류 : GET, POST, PUT, DELETE...
- 서버가 수행해야 할 동작 지정

<mark>응답 메시지 : HTTP/1.1 200 OK content-Type: text/html;charset=UTF-8 Content-Length: 3423 .. 태그들 </mark>

- HTTP 버전
- HTTP 상태코드 : 요청 성공, 실패를 나타냄
  - 200 : 성공
  - 400 : 클라이언트 요청 오류
  - 500 : 서버 내부 오류
- 이유 문구 : 사람이 이해할 수 있는 짦은 상태 코드 설명 글

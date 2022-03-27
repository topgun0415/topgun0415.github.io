---
layout: post
title: 모든 개발자를 위한 HTTP 기본지식 6편 🌐
date: 2022-03-27 14:00 +0800
# last_modified_at: 2022-02-16 01:08:25 +0800
tags: [http]
toc: true
math: false
---

![lecture](https://cdn.inflearn.com/public/courses/326277/cover/52d4f143-b470-4109-96cb-a0b146fb42ed/http.png)

# HTTP Header 1 - 일반 헤더

## 💬 HTTP 헤더 개요

### 용도

- HTTP 전송에 필요한 모든 부가정보
- 예) 메시지 바디의 내용, 메시지 바디의 크기, 압축, 인증, 요청 클라이언트, 서버 정보, 캐시 관리 정보..
- 표준 헤더가 너무 많음
- 필요시 임의의 헤더 추가 기능

### 분류

- 헤더 분류
  - General 헤더 : 메시지 전체
  - Request 헤더 : 요청 정보
  - Response 헤더 : 응답 정보 : Server, Apache
  - Entity 헤더 : 엔티티 바디 정보 : Content-Type

### HTTP BODY

- 메시지 본문은 엔티티 본문을 전달하는데 사용
- 엔티티 본문은 요청이나 응답에서 전달할 실제 데이터
- 엔티티 헤더는 엔티티 본문의 데이터를 해석할 수 있는 정보 제공
  - 데이터 유형(html,json), 데이터 길이, 압축 정보 등등

### HTTP BODY(최신 스펙)

- 메시지 본문을 통해 표현 데이터 전달
- 메시지 본문 = 페이로드
- 표현은 요청이나 응답에서 전달할 실제 데이터
- 표현 헤더는 표현 데이터를 해석할 수 있는 정보 제공
  - 데이터 유형(html,json), 데이터 길이, 압축 정보 등등
- 참고 : 표현 헤더는 표현 메타데이터와, 페이로드 메시지를 구분해야 하지만..

---

## 💡 표현

- Content-Type : 표현 데이터의 형식
- Content-Encoding : 표현 데이터의 압축 방식
- Content-Language : 표현 데이터의 자연 언어
- Content-Length : 표현 데이터의 길이

- 표현 헤더는 전송, 응답 둘다 사용

### Content-Type

표현 데이터의 형식 설명

- 미디어 타입, 문자 인코딩
- 예)
  - text/html; charset=utf-8
  - application/json
  - image/png

### Content-Encoding

표현 데이터 인코딩

- 표현 데이터를 압축하기 위해 사용
- 데이터를 전달하는 곳에서 압축 후 인코딩 헤더 추가
- 데이터를 읽는 쪽에서 인코딩 헤더의 정보로 압축 해제
- 예)
  - gzip
  - deflate
  - identity

### Content-Language

표현 데이터의 자연언어

- 표현 데이터의 자연 언어 표현
- 예)
  - ko
  - en
  - jp
  - en-US

### Content-Length

표현 데이터의 길이

- 바이트 단위
- Transfer-Encoding(전송 코딩)을 사용하면 Content-Length를 사용하면 안됨

---

## 👥 콘텐츠 협상 (Content Negotiation)

클라이언트가 선호하는 표현 요청 그리고 서버는 그것을 최대한 응답해서 해보려고 하는 노력

- Accept : 클라이언트가 선호하는 미디어 타입 전달
- Accept-Charset : 클라이언트가 선호하는 문자 인코딩
- Accept-Encoding : 클라이언트가 선호하는 압축 인코딩
- Accept-Language : 클라이언트가 선호하는 자연 언어

- 협상 헤더는 요청시에만 사용

### 협상과 우선순위 1

Quality Values(q)

<mark>예시</mark> 내가 들어가고 싶은 사이트가 있는데 Accept-Language에 kr을 요청했다고 가정하자. 근데 그 사이트에서는 fr(프랑스어)가 기본어고 영어가 옵션이라고 한다면 서버에서는 영어보다는 기본어인 프랑스어를 지원해줄 가능성이 높다.

- 0~1, 클수록 높은 우선순위
- 생략하면 1
- Accept-Language: ko-KR,ko;q=0.9,en-US;q=0.8,en:q=0.7
  - ko-KR;q=1
  - ko;q=0.9
  - en-US;q=0.8
  - en;q=0.7

### 협상과 우선순위 2

- 구체적인 것이 우선한다.
- Accept : text/\*, text/plain 등등

### 협상과 우선순위 3

- 구체적인 것을 기준으로 미디어 타입을 맞춘다

---

## 📡 전송방식

- 단순 전송 : Content-Length 값을 알고 주는 것
- 압축 전송 : 서버에서 압축하여서 보낼 시 Content-Encoding 값을 보내줘야 함
- 분할 전송 : Transfer-Encoding을 추가하여서 분할로 전송하여 용량을 최소한으로 해서 클라이언트가 잘라서 받아 볼 수 있게 한다. (Content-Length ❌)
- 범위 전송 : 이미지를 받는데 중간에 멈쳤을 경우 받은 곳부터 명시해서 다시 나머지를 받도록 하는 것

---

## 📄 일반정보

### From

유저 에이전트의 이메일 정보

- 일반적으로 잘 사용되지 않음
- 검색 엔진 같은 곳에서, 주로 사용
- 요청해서 사용

### Referer

현재 페이지를 타고 오게끔 한 이전 웹 페이지 주소

- 현재 요청된 페이지의 이전 웹 페이지 주소
- A -> B로 이동하는 경우 B를 요청할 때 Feferer : A를 포함해서 요청
- Referer를 사용해서 유입 경로 분석 가능
- 요청에서 사용
- 참고 : referer는 단어 referrer의 오타 ㅋㅋ

### User-Agent

웹 브라우저 정보 및 클라이언트 어플리케이션 정보

- 통계 정보
- 어떤 종류의 브라우저에서 장애가 발생하는지 파악 가능
- 요청에서 사용

### Server

요청을 처리하는 ORIGIN 서버의 소프트웨어 정보

- Server : Apache/2.2.22 (Debian)
- server: nginx
- 응답에서 사용

### Date

메시지가 발생한 날짜와 시간

- 응답에서만 사용

---

## ℹ️ 특별한 정보

### Host

요청한 호스트 정보(도메인)

- 요청에서 사용
- 호스트 정보는 필수!!!
- 하나의 서버가 여러 도메인을 처리해야 할 때
- 하나의 IP 주소에 여러 도메인이 적용되어 있을 때

### Location

페이지 리다이렉션

- 웹 브라우저는 3xx 응답의 결과에 Location 헤더가 있으면, Location 위치로 자동 이동
- 201 (Created): Location 값은 요청에 의해 생성된 리소스 URI
- 3XX (Redirection): Location 값은 요청을 자동으로 리디렉션 하기 위한 대상 리소스를 가리킴

### Allow

허용 가능한 HTTP 메서드

- 405(Method Not Allowed)에서 응답에 포함해야함

- Allow: GET, HEAD, PUT

### Retry-After

유저 에이전트가 다음 요청을 하기까지 기다려야하는 시간

- 503(Service Unavailable): 서비스가 언제까지 불능인지 알려줄 수 있음

---

## ✔️ 인증

### Authorization

클라이언트 인증 정보를 서버에 전달

### WWW-Authenticate

리소스 접근시 필요한 인증 방법 정의

- 리소스 접근시 필요한 인증 방법 정의
- 401 Unauthorized 응답과 함께 사용

---

## 🍪 쿠키

- Set-Cookie = 서버에서 클라인트로
- Cookie = 클라이언트에서 서버로

<mark>Server is Stateless!</mark>

모든 요청에 정보를 넘기는 문제

- 모든 요청에 사용자 정보가 포함되도록 개발 해야함
- 브라우저를 완전히 종료하게 되면?

이런 문제들을 해결하기 위해서 쿠키가 만들어짐

### 쿠키 정의

예시)

```
set-cookie: seesionId=abcde1234; expires=Sat,26-Dec-2020 00:00:00 GMT; path=/; domain=.google.com; Secure
```

- 사용처

  - 사용자 로그인 세션 관리 : 서버에서 세션 키를 만들어서 세션 값을 클라이언트에게 반환함
  - 광고 정보 트래킹

- 쿠키 정보는 항상 서버에 전송됨

  - 네트워크 트래픽 추가 유발
  - 최소한의 정보만 사용(세션 id, 인증 토큰)
  - 서버에 전송하지 않고, 웹 브라우저 내부에 데이터를 저장하고 싶으면 웹 스토리지(localStorage, sessionStorage) 참고

- ⚠️ 주의
  - 보안에 민감한 데이터는 저장하면 안됨(주민번호, 신용카드 번호)

### 쿠키 - 생명주기

Expires, max-age

- Set-Cookie : expires=Sat,26-Dec-2020 04:39:21 GMT

  - 만료일이 되면 쿠키 삭제

- Set-Cookie : max-age=3600(3600초)

  - 0이나 음수를 지정하면 쿠키 삭제

- 세션 쿠키 : 만료 날짜를 생략하면 브라우저 종료시 까지만 유지
- 영속 쿠키 : 만료 날짜를 입력하면 해당 날짜까지 유지

### 쿠키 - 도메인

- 예) domain=example.org
- 명시 : 명시한 문서 기준 도메인 + 서브 도메인 포함
- 생략 : 현재 문서 기준 도메인만 적용

### 쿠키 - 경로

- 예) path=/home
- 이 경로를 포함한 하위 경로 페이지만 쿠키 접근
- 일반적으로 path=/루트로 지정
- 예)
  - path=/home 지정
  - /home 가능
  - /home/level1 가능
  - /home/level1/level2 가능
  - /hello 불가능

### 쿠키 - 보안

- Secure

  - 쿠키는 http, https를 구분하지 않고 전송
  - Secure를 적용하면 https인 경우에만 전송

- HttpOnly

  - XSS 공격 방지
  - 자바스크립에서 접근 불가
  - HTTP 전송에만 사용

- SameSite
  - XSRF 공격 방지
  - 요청 도메인과 쿠키에 설정된 도메인이 같은 경우만 쿠키 전송

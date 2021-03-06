---
layout: post
title: 모든 개발자를 위한 HTTP 기본지식 3편 🌎
date: 2022-03-22 11:00 +0800
# last_modified_at: 2022-02-16 01:08:25 +0800
tags: [http]
toc: true
math: false
---

![lecture](https://cdn.inflearn.com/public/courses/326277/cover/52d4f143-b470-4109-96cb-a0b146fb42ed/http.png)

# HTTP 메서드

## 🍳 HTTP API를 만들어보자

처음으로 HTTP API를 만들어보자! 😅

요구사항 : 회원 정보 관리 API를 만들어라

- 회원 목록 조회 /read-member-list
- 회원 조회 /read-member-by-id
- 회원 등록 /create-member
- 회원 수정 /update-member
- 회원 삭제 /delete-member

이것이 좋은 URI 설계일까?

⭐ 가장 중요한 것은 <mark>리소스 식별</mark>

API URL 고민

- 리소스의 의미는 뭘까?
  - 회원을 등록하고 수정하고 조회하는게 리소스가 아니다!
  - 회원이라는 개념 자체가 바로 리소스다.
- 리소스를 어떻게 식별하는게 좋을까?
  - 회원을 등록하고 수정하고 조회하는 것을 모두 배제
  - <mark>회원이라는 리소스만 식별하면 된다. -> 회원 리소스를 URI에 매핑</mark>

⭐ API URL 설계 : 리소스 식별, URI 계층 구조 활용

- 회원목록조회 /members
- 회원 조회 /members/{id}
- 회원 등회 /members/{id}
- 회원 수정 /members/{id}
- 회원 삭제 /members/{id}

조회부터 삭제까지 어떻게 구별할까?

⭐ 리소스와 행위을 분리해야 한다!
<mark>가장 중요한 것은 리소스를 식별하는 것</mark>

- URI는 리소스만 식별!
- 리소스와 해당 리소스를 대상으로 하는 행위를 분리
  - 리소스: 회원
  - 행위: 조회, 등록, 삭제, 변경
- 리소스는 명사, 행위는 동사 (미네랄을 캐라)
- 행위(메서드는)는 어떻게 구별하나?

---

## ⭐ HTTP 메서드

### 메서드 종류 (주요 메서드)

- GET : 리소스 조회
- POST : 요청 데이터 처리, 주로 등록에 사용
- PUT : 리소스를 대체, 해당 리소스가 없으면 생성 (파일 생성과 비슷)
- PATCH : 리소스 부분 변경
- DELETE : 리소스 삭제

### 기타 메서드

- HEAD : GET과 동일하지만 메시지 부분을 제외하고, 상태 줄과 헤더만 반환
- OPTIONS : 대상 리소스에 대한 통신 가능 옵션을 설명 (주로 CORS에서 사용)
- CONNECT : 대상 자원으로 식별되는 서버에 대한 터널을 설정
- TRACE : 대상 리소스에 대한 경로를 따라 메시지 루프백 테스트를 수행

---

### GET 🔬

데이터를 요청하는 것

- 리소스 조회
- 서버에 전달하고 싶은 데이터는 query를 통해서 전달
- 메시지 바디를 사용해서 데이터를 전달할 수 있지만, 지원하지 않는 곳이 많아서 권장하지 않음

### POST 📮

- 요청 데이터 처리
- 메시지 바디를 통해 서버로 요청 데이터 전달
- 서버는 요청 데이터를 처리
  - 메시지 바디를 통해 들어온 데이터를 처리하는 모든 기능을 수행한다.
- 주로 전달된 데이터로 신규 리소스 등록, 프로세스 처리에 사용

예시 : HTML , FORM 입력한 정보로 회원가입, 주문, 게시판 글쓰기, 댓글 달기 , 신규 주문 생성

### PUT ✏️

파일에 폴더를 집어넣는 것과 똑같음.

- 리소스를 대체
  - 리소스가 있으면 대체
  - 리소스가 없으면 생성
  - 쉽게 이야기해서 덮어버림

⭐ 중요! 클라이언트가 리소스를 식별

- 클라이언트가 리소스 위치를 알고 URI 지정
- POST와 차이점(POST는 PUT처럼 정확한 PATH를 지정 안해줘도 됨)

🔴 주의! 리소스를 완전히 대체하므로 조심해야함

### PATCH 📬

PUT과 반대로 어떤 특정 리소스 부분만 변경하고 싶을 때는 PATCH 사용하면 됨

### DELETE ❌

리소스를 제거하기 위해서는 DELETE 사용

---

## ⭐ HTTP 메서드의 속성

### 안전 Safety 🧷

- 호출해도 리소스를 변경하지 않는다.
- Q : 그래도 계속 호출해서, 로그 같은게 쌓여서 장애가 발생하면요?
- A : 안전은 해당 리소스만 고려한다. 그런 부분까지 고려하지 않는다.

### 멱등 Idempotent

- f(f(x)) = f(x)
- 한 번 호출하든 두 번 호출하든 100번 호출하든 결과가 똑같다.
- 멱등 메서드
  - GET : 한 번 조회하든, 두번 조회하든 같은 결과가 조회한다.
  - PUT : 결과를 대체한다. 따라서 같은 요청을 여러번 해도 최종 결과는 같다/
  - DELETE : 결과를 삭제한다. 같은 요청을 여러번 해도 삭제된 결과는 똑같다.
  - POST : 멱등이 아니다! 두 번 호출하면 같은 결제가 중복해서 발생 할 수 있다.

활용 : 자동 복구 매커니즘. 서버가 TIMEOUT 등으로 정상 응답을 못 주었을 때, 클라이언트가 같은 요청을 다시 해도 되는가 판단

💡 재요청 중간에 다른 곳에서 리소스를 변경해버리면 ?
멱등은 외부 요인으로 중간에 리소스가 변경되는 것 까지는 고려하지는 않는다.

### 캐시가능 Cacheable ♟️

- 응답 결과 리소스를 캐시해서 사용해도 되는가?
- GET, HEAD, POST, PATCH 캐시 가능
- 실제로는 GET, HEAD 정도만 캐시로 사용
  - POST, PATCH는 본문 내용까지 캐시 키로 고려해야 하는데 구현이 쉽지 않음

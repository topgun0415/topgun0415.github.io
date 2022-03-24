---
layout: post
title: 모든 개발자를 위한 HTTP 기본지식 4편 🌐
date: 2022-03-24 23:00 +0800
# last_modified_at: 2022-02-16 01:08:25 +0800
tags: [http]
toc: true
math: false
---

![lecture](https://cdn.inflearn.com/public/courses/326277/cover/52d4f143-b470-4109-96cb-a0b146fb42ed/http.png)

# HTTP 메서드 활용

## 🧑‍💻 -> 🗃️ 클라이언트에서 서버로 데이터 전송

- 쿼리 파라미터를 통한 데이터 전송

  - GET
  - 주로 정렬 필터(검색어)

- 메시지 바디를 통한 데이터 전송
  - POST, PUT, PATCH
  - 회원가입, 상품 주문, 리소스 등록, 리소스 변경

### 정적 데이터 조회

쿼리 파라미터 미사용

- 이미지, 정적 텍스트 문서
- 조회는 GET 사용
- 정적 데이터는 일반적으로 쿼리 파라미터 없이 리소스 경로로 단순하게 조회 가능

### 동적 데이터 조회

- 주로 검색, 게시판 목록에서 필터(검색어)
- 조회 조건을 줄여주는 필터, 조회 결과를 정렬하는 정렬 조건에 주로 사용
- 조회는 GET 사용
- GET은 쿼리 파라미터 사용해서 데이터를 전달

⚠️ GET에도 바디 메세지를 넣을 수는 있지만 권장하지는 않음

### HTML Form 데이터 전송

POST 전송 - 저장
GET 전송 - 저장
multipart/form-data - 파일 업로드 같은 바이너리 데이터 전송시 사용

❗ HTML Form 전송은 GET, POST만 지원

### HTTP API 데이터 전송

- 서버 to 서버 : 백엔드 시스템 통신
- 앱 클라이언트 : 아이폰 , 안드로이드
- 웹 클라이언트 : HTML에서 Form 전송 대신 자바 스크립트를 통한 통신에 사용(AJAX)
- POST PUT PATCH : 메시지 바디를 통해 데이터 전송
- GET : 조회, 쿼리 파라미터로 데이터 전달
- Content-type : application/json을 주로 사용(사실상 표준)
  - TEXT, XML, JSON 등등

### ✨ 클라이언트에서 서버로 데이터 전송 (정리)

<mark>데이터 전달 방식은 크게 2가지</mark>

- ⭐ 쿼리 파라미터를 통한 데이터 전송

  - GET
  - 주로 정렬 필터(검색어)

- ⭐ 메시지 바디를 통한 데이터 전송

  - POST, PUT, PATCH
  - 회원가입, 상품 주문, 리소스 등록, 리소스 변경

⭐ 정적데이터 조회 : 이미지, 정적 텍스트

⭐ 동적데이터 조회 : 주로 검색, 게시판 목록에서 정렬필터

⭐ HTML Form을 통한 데이터 전송 : 회원가입, 상품주문, 데이터변경

⭐ HTTP API를 통한 데이터 전송 : 회원가입, 상품주문, 데이터변경, 서버 to 서버, 앱 클라이언트, 웹 클라이언트

---

## 🔧🔨 HTTP API 설계 예시

### HTTP API - 컬렉션

⭐ 회원 관리 시스템

- 회원 목록 /members -> GET
- 회원 등록 /members -> POST
- 회원 조회 /members/{id} -> GET
- 회원 수정 /members/{id} -> PATCH,PUT,POST
- 회원 삭제 /members/{id} -> DELETE

⭐ POST - 신규 자원 등록 특징

- 클라이언트는 등록될 리소스의 URL을 모른다.

  - 회원 등록 /members -> POST
  - POST /members

- 서버가 새로 등록된 리소스 URI를 생성해준다.

  - HTTP/1.1 201 Created
  - Location : /members/100

- 컬렉션(Collection)
  - 서버가 관리하는 리소스 디렉토리
  - 서버가 리소스의 URL를 생성하고 관리
  - 여기서 컬렉션은 /members

### HTTP API - 스토어

⭐ 파일 관리 시스템 : API 설계 - PUT 기반 등록

- 파일 목록 /files -> GET
- 파일 조회 /files/{filename} -> GET
- 파일 등록 /files/{filename} -> PUT
- 파일 삭제 /files/{filename} -> DELETE
- 파일 댕략 등록 /files -> POST

클라이언트가 리소스 URI를 알고 있어야 한다.

클라이언트가 직접 리소스의 URI를 지정해야한다.

<mark> 즉 POST가 서버에 요청한다는 것은 서버가 만들어주고 응답 메시지로 ID나 URI를 알려준다 하지만 PUT은 클라이언트가 정확히 어디에 수정할건지 PATH를 알고 있어야한다 </mark>

⚠️ 실무에서는 대부분 POST가 사용되지 PUT이 사용되는 곳은 극히 드물다.

### HTML FORM 사용

- HTML FORM은 <mark>GET, POST만 지원</mark>
- AJAX같은 기술을 사용해서 해결 가능
- 순수 HTML, HTML FORM을 사용하면 GET, POST 밖에 사용 불가능

- 회원 목록 /members -> GET
- 회원 등록 폼 /members/new -> GET
- 회원 등록 /members/new,/members -> POST
- 회원 조회 /members/{id} -> GET
- 회원 수정 폼 /members/{id}/edit -> GET
- 회원 수정 /members/{id}/edit, /members/{id} -> POST
- 회원 삭제 /members/{id}/delete -> POST

⭐ 컨트롤 URI : HTML FORM은 GET, POST만 지원이 가능하므로 어쩔 수 없이 동사 URI를 사용함

- GET, POST만 지원하므로 제약이 있음
- 이런 제약을 해결하기 위해 동사로 된 리소스 경로 사용
- POST의 /new, /edit, /delete가 컨트롤 URI
- HTTP 메서드로 해결하기 애매한 경우 사용(HTTP API 포함)

### 정리

- HTTP API - 컬렉션

  - POST 기반 등록
  - 서버가 리소스 URI 결정

- HTTP API - 스토어

  - PUT 기반 등록
  - 클라이언트가 리소스 URI 결정

- HTML FORM 사용
  - 순수 HTML + HTML form 사용
  - GET, POST만 지원

⭐ 리소스 네이밍 참고사이트 : https://restfulapi.net/resource-naming

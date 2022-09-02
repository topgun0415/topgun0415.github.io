---
layout: post
title: Servlet ☕
date: 2022-09-03 02:00 +0800
# last_modified_at: 2022-02-16 01:08:25 +0800
tags: [web, java]
toc: true
math: false
---

![Java](https://janikvonrotz.ch/wp-content/uploads/2014/10/Java-logo.jpg)

## 🫙 Servlet이란

서블릿(Servlet)이란 클라이언트로부터 요청을 처리하고, 그 결과를 클라이언트에게 다시 반환해주는 웹 프로그래밍 기술이다. 그리고 이는 서버사이드 언어인 자바를 사용하여 프로그래밍한다.

오래전 웹은 클라이언트에서 요청이 오면 그 결과를 일일이 정적으로 만들어서 보내줘야하는 노오오력이 필요한 작업들이 요구되었다. 특히나 일일이 개발자가 클라이언트가 입력한 정보도 코드 한줄 한줄로 쳐서 결과값을 띄워주거나 하는 매우 번거로운 작업들이 필요했다. 🤪

하지만 웹 프로그래밍이 점점 발전하면서 클라이언트의 요청에 알맞게 동적으로 페이지를 작성할 수 있게 되었다. 즉 유저와 상호작용이 가능하게 된 것이다!

![HTTP Message](https://user-images.githubusercontent.com/49539592/135721043-123ddb7e-507d-4b43-8bdc-e91679e64621.png)

위의 사진은 HTTP 요청(Request)와 응답(Response) 메세지이다. 딱 봐도 귀찮아 보이고 요청받기 싫게 생기지 않았나?? 😨

개발자가 일일이 이를 해석하고 사용하려고 하면 매우 번거롭고 긴 시간이 필요할 것이다. 하지만 이 귀찮은 일을 서블릿이 대신 해준다!!

그러므로 <mark>서블릿이란 좋은 녀석은 개발자들이 오로지 로직을 짜는데에만 집중하게 만들어준다.</mark>

---

![Servlet](https://blog.kakaocdn.net/dn/bwYPt3/btqD0OaASQP/OhsfjdeZkNKVb2bms48Lfk/img.png)

위 사진은 /HelloWorld의 URL이 호출되면 서블릿 코드가 실행된다. @WebServlet("/HelloWorld")라고 적혀있는 부분이 url과 Servlet을 연결해준다고 생각하자.

그리고 HTTP 요청 정보를 사용 할 수 있는 HttpServletRequest와 응답 정보를 사용할 수 있는 HttpServletResponse가 있다. 아 물론 클라이언트로부터 어떠한 HTTP 통신방법으로 온건지에 따라서 실행되는 doGet 혹은 doPost가 실행되긴하지만 말이다. 😅

밑에 사진은 Servlet과 Servlet Container의 구동 원리이다.

![Servlet Container](https://cdn.inflearn.com/public/files/posts/8ffb96d5-4d8c-4e08-a4c1-bfb418508f4d/blob)

## ⚙️ Servlet의 동작 방식

- 사용자가 해당 url(예시 : localhost://8080/helloServlet)로 접속을 하면 HTTP Request가 Servlet Container로 전송

- 클라이언트단의 요청을 전송받은 Servlet Container는 HttpRequest, HttpResponse 객체를 생성한다.

- 사용자가 요청한 url이 어느 서블릿에 대한 요청인지 서블릿 컨테이너는 web.xml을 통해 찾게 된다.

- 클라이언트의 GET, POST 둘 중 어떤 REST API로 요청이 들어온건지 doGet(), doPost()이 호출된다.

- 클라이언트로 받은 정보들을 서블릿에서 1차 가공 후 Bean 혹은 JSP로 스코프를 통해 넘겨준다. Forwarding이라는 것도 있다.

- Bean을 통해 사용자가 요청한 정보중에 데이터베이스에서 가져올 정보들이 있으면 2차로 정보를 가공한다.

- 최종적으로는 View를 맡고 있는 JSP 등의 동적 페이지를 생성한 후 HttpServletResponse 객체에 응답을 보낸다.

- 클라이언트가 해당 응답을 받았으면 HttpServletRequest, HttpServletResponse 객체를 소멸한다.

## ♻️ Servlet의 라이프사이클

- 클라이언트 요청이 들어오면 컨테이너는 서블릿이 메모리에 있는지 확인하고 메모리에 없다면 init() 메서드를 호출하여 적재

- 클라이언트 요청에 따라 Service() 메소드를 통해 요청에 대한 응답이 doGet(), doPost()로 나눠지고 HttpServletRequest, HttpServletResponse에 의해 request와 response 객체가 제공된다.

- 컨테이너 서블릿에 종료 요청을 하면 destroy() 메서드가 호출된다. 종료시 처리해야하는 로직이 있다면 destroy() 메서드를 오버라이딩하면 된다.

## 📦 Servlet Container

서블릿 컨테이너는 스스로 동작하지 않는 서블릿을 관리해주는 컨테이너다. <mark>서블릿 컨테이너는 클라이언트의 요청을 받고 응답할 수 있도록 웹 서버와 소켓으로 통신한다. 톰캣이 서블릿 컨테이너의 대표적인 예이다.</mark>

### ⚠️ Servlet Container의 역할 및 특징

- 톰캣처럼 서블릿을 지원하는 WAS(Web Application Server)를 서블릿 컨테이너라 한다.
- 서블릿 객체를 생성, 초기화, 호출, 종료까지 관리해주는 라이프사이클 관리
- 서블릿 객체는 싱글톤으로 관리
- 동시 요청을 병렬 처리하기위한 멀티쓰레드 지원 가능

---
layout: post
title: Database & MySQL Basic 🐬
date: 2022-09-08 22:00 +0800
# last_modified_at: 2022-02-16 01:08:25 +0800
tags: [db]
toc: true
math: false
---

![Java](https://cdn.inflearn.com/public/courses/327501/cover/8244ef74-09f3-4776-8893-b9cfefa22a18/%EC%8D%B8%EB%84%A4%EC%9D%BC_mysql_2%20%EB%B3%B5%EC%82%AC.png)

인프런에서 강의를 구입하고 제가 알아보기 쉽게 복습하는 용도로 작성합니다.

## RDBMS (Relational Database Management System) 🛢

관계형 데이터베이스 관리시스템이라고 한다. 우선 기본적으로 MySQL은 RDBMS의 한 종류이다.

## What is Database ?

데이터베이스라는 것은 어떤 한 위치에 정보를 저장해뒀다가 어디든 사용가능할 수 있게 내려주는 그런 시스템이다. 즉 특정 소프트웨어나 프로그램에 종속되지 않고 독립된 정보의 집합 내지 저장소이다. 데이터베이스라는 것 자체는 사실 비어있는 캐비넷이나 창고와 다름없는 존재이다. 하지만 필요한 정보들을 집어놓고 명령문으로 필요할때마다 적시적소에 내려주는 정보 자판기로 만들게 되면 그것이 바로 DBMS(Database Management System)라는 것이 된다.

그리고 각 데이터베이스는 사용자가 정보를 입력하고 조회하고 수정, 삭제하는 등의 데이터를 관리할 수 있는 방식이 있는데 MySQL을 비롯해서 다수의 데이터베이스들은 그 방식으로 SQL을 사용한다.

## SQL vs NoSQL

현재 데이터베이스의 종류인 SQL과 NoSQL를 비교하면서 기록하려 한다! 😋

![sqlVSno-sql](https://kciter.so/images/2021-02-25-about-mongodb/mongodb-layer.jpg)

### NoSQL

NoSQL로 유명한 MongoDB

![mongoDB](https://www.howtogeek.com/wp-content/uploads/csit/2021/07/f5932bc2.jpg?height=200p&trim=2,2,2,2)

해쉬테이블과 같은 방식인 KEY와 VALUE로 저장한다.

![mongoDB2](https://webimages.mongodb.com/_com_assets/cms/1-lwnlfl1ryn.png?auto=format%2Ccompress&ch=DPR)

예시로 어떤 백화점에 푸드코트가 있고, 거기서 사먹을 수 있는 모든 메뉴들의 정보를 데이터베이스로 정리하려고 한다.
MongoDB와 같이 NoSQL은 기본적으로 각 음식들마다 저장할 수 있는 정보가 상당히 자유롭다. MySQL은 가격, 맛, 평가도와 같이 모든 음식들이 똑같은 항목들을 바탕으로 작성해나가야 한다면 MongoDB에서도 크게 다르지는 않으나 각 음식들 마다 평가도라는 항목이 어떤 곳에는 인기도 혹은 평판 등의 항목들로 적혀질 수 있다는 점이 있다. 그러므로 자유로울뿐더러 빠르게 정보를 받아올 수 있는 장점들이 있으나 반대로 자유에서 오는 편안함은 나중에 반대로 불편함이 야기될 수도 있기 때문에 서로 각 장단점이 존재한다.

---

### SQL

SQL을 사용하는 다양한 데이터베이스들이 있지만 대표격인 MySQL

![mySQL](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQRDMUOiHFCmW69kq-2bbGiylFVivImzNvLQQ&usqp=CAU)

MySQL의 저장방식은 우리가 흔히아는 엑셀과 상당히 유사하다.

![Excel](https://t1.daumcdn.net/cfile/tistory/26627642575E854702)

행과 열에 이름을 붙임으로서 정보를 보다 보기 쉽게 테이블로 만든다. 그리고 어떤 데이터들은 숫자 혹은 텍스트로만 타입을 한정해서 더 효율적으로 만들어준다.
그리고 이런 테이블들을 새로 만들고, 조회하고, 삭제하고, 수정하는 그 단축키가 바로 SQL인 것이다.

![mySQLCode](https://cphinf.pstatic.net/mooc/20220723_117/1658585292628EgmJL_PNG/mceclip0.png)

또한 데이터베이스들은 테이블을 작성하다보면 중복되는 데이터들이 많을 수 있으니 각자 고유의 ID값을 부여할 뿐만 아니라 어떠한 정보들끼리 관계를 맺게 함으로써 모든 데이터들이 유기적으로 중복없이 잘 가르키게 되어진다. 물론 효율적인 정보를 관리하기 위해서는 오랜 노력과 설계능력이 필요한 부분이니 이건 공부하면서 익혀나가도록 하자! 🤪

---
layout: post
title: 제대로 파는 Git & Github 4 🐙
date: 2022-03-21 13:00 +0800
# last_modified_at: 2022-02-16 01:08:25 +0800
tags: [git]
toc: true
math: false
---

![Git & Github](https://blog.kakaocdn.net/dn/obZjH/btqF3b8YFA8/m1c8xWYH0uAz7PVkt3q8M0/img.png)

# Github 사용하기 🐙 + 😸

## 🐰 GitHub은 뭐고 왜 쓰나요?

### 팀원들과 협업하기 위한 깃헙에 대해서 알아보자!

Github는 Git으로 관리되는 모든 프로젝트들을 온라인 공간에 공유해서 프로젝트 구성원들이 함께 소프트웨어를 만들 수 있도록 도와주는 서비스다.

---

### 일반 클라우드 서비스와는 무엇이 다른 것일까?

구성원들이 한번에 한번씩만 작업을 하게 되고 그 작업이 완료가 되면 업로드를 한 다음에 다음 구성원이 작업을 마치고, 해당 작업을 다운로드하여 작업을 마친 뒤 업로드 하는 방식이라면 전혀 문제될 것이 없지만 이렇게 사용하는거면 협업이라는 의미 자체가 없어진다. 또한 동시에 작업하려고 서로 다른 기능들을 수정해서 업로드 하기 시작하면 무조건 해당 프로젝트는 꼬이기 시작할 것이다.

모든 팀원들이 같은 시간에 출근해서 어떤 한 프로젝트를 동시에 작업을 할 수 있어야한다. 그리고
동시에 한 파일을 여러명이서 수정할 수 있도록 할 수 있게 해줘야 한다.

💡 이러한 기능들을 Github에서는 정말 깔끔하게 처리할 수 있도록 해준다.

🛑 Github과 Git에서는 모든 업로드와 다운로드를 커밋 단위로 주고 받는다. 그리고 깃헙은 모든 프로젝트의 최근 업로드 시킨 그 파일을 적용시키고 다운로드도 최신의 업로드 버전을 강제로 적용시키게 한다. 그리고 나서 추가로 .git 파일에 있는 log 내역들을 이용해서 과거, 차원 이동등이 가능하도록 한다.

---

## 💾 원격 저장소 사용하기

### 로컬에 원격 저장소 추가 후 푸시

GitHub 레포지토리 생성 후 복붙 명령어

```
git remote add origin (원격 저장소 주소)
```

- 로컬의 Git 저장소에 원격 저장소로의 연결 추가
  - 원격 저장소 이름에 흔히 origin 사용. 다른 것으로 수정 가능

```
git branch -M main
```

- GitHub 권장 - 기본 브랜치명을 main으로

```
git push -u origin main
```

- 로컬 저장소의 커밋 내역들 원격으로 push(업로드)
  - -u 또는 --set-upstream : 현재 브랜치와 명시된 원격 브랜치 기본 연결

---

### ⭐️ GitHub의 해당 레포지토리 페이지 새로고침하여 살펴보기

원격 목록 보기

```
git remote
```

지우기 (로컬 프로젝트와의 연결만 없애는 것, 레포는 무관)

```
git remote remove (origin 등 원격 이름)
```

---

### GitHub에서 프로젝트 다운받기

터미널이나 Git Bash에서 대상 폴더 이동 후

```
git clone (원격 저장소 주소)
```

---

## ⏩ push와 pull

### 원격으로 커밋 밀어올리기(push)

홈페이지 보고 실습

아래 명령어로 push

```
git push
```

- 이미 git push -u origin main으로 대상 원격 브랜치가 지정되었기 때문에 가능

이후 Github 페이지에서 새로고침 하면 커밋 내용과 함께 확인 가능

---

### 원격의 커밋 당겨오기(pull)

홈페이지 보고 실습

아래 명령어로 pull

```
git pull
```

Pull을 실행하면 로컬에서 파일과 log에서 변경된 점 확인 가능

---

### pull 할 것이 있을 때 push를 하면?

혹시나 로컬에서 push를 하려고 할 때 원격에서 push가 이미 되어서 새 버전이 있다면 어떻게 될까?

push 할 것이 있을 시 pull 하는 두 가지 방법

1. git pull --no-rebase - merge 방식

   - 소스트리에서 확인해보기
   - reset으로 되돌린 다음 아래 방식도 해보기

2. git pull --rebase - rebase 방식

   - pull 상의 rebase는 다름 (협업시 사용 OK)

다 끝나면 push 하기

👾 이부분에서 충돌이 발생했다면?

영상에서와 같이, manager 줄과 coach 줄 사이에 빈 줄이 하나 있는지 확인하세요.
Git은 같은 파일의 같은 부분에 양쪽에서 수정사항이 있을 때 이를 충돌로 인식

```
...
manager: Dooli
(빈 줄 - 윗부분과 아랫부분을 나눠주는 경계가 됨)
coach: Lupi
...
```

영상처럼 빈 줄을 넣으셨다면 이것이 manager 부분과 coach 부분의 경계로 작용하지만
이들을 붙여서 넣으셨다면 한 부분으로 인식되어 충돌로 분류되어짐

---

### 💣 협업상 충돌 발생 해결하기

1. 로컬에서 Panthers에 Maruchi 추가

   - 커밋 메시지: Add Maruchi to Panthers

2. 원격에서 Panthers에 Arachi 추가

   - 커밋 메시지: Add Arachi to Panthers

3. pull 하여 충돌상황 마주하기

--no-rebase와 --rebase 모두 해 볼 것

---

### 로컬의 내역 강제 push해보기

1. 로컬의 내역 충돌 전으로 reset

2. 아래 명령어로 원격에 강제 적용

```
git push --force
```

---

## 🎄 원격의 브랜치 다루기

### 로컬에서 브랜치 만들어 원격에 push 해보기

1. from-local 브랜치 만들기

2. 아래 명령어로 원격에 push

아래와 같이 하면 대상을 명시하라는 메시지 나타남

```
git push
```

아래 명령어로 원격의 브랜치 명시 및 기본설정

```
1. git push -u origin from-local
2. push하고 나오는 메세지로도 remote 설정 가능
```

3. 브랜치 목록 살펴보기
   - GitHub에서 목록 보기
   - 아래 명령어로 로컬과 원격의 브랜치들 확인

---

### 원격의 브랜치 로컬에 받아오기

1. GitHub에서 from-remote 브랜치 만들기

   - git branch -a에서 현재는 보이지 않음

2. 아래 명령어로 원격의 최신 변경사항 받아오기

```
git fetch
```

    - git brahcn -a로 확인

3. 아래 명령어로 로컬에 같은 이름의 브랜치를 생성하여 연결하고 switch(생성,연결,switch)

```
git switch -t origin/from-remote
```

---

### 원격의 브랜치 삭제

```
git push (원격 이름) --delete (원격의 브랜치명)
```

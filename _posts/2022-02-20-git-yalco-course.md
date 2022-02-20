---
layout: post
title: 제대로 파는 Git & Github 1 🐙
date: 2022-02-20 18:00 +0800
# last_modified_at: 2022-02-16 01:08:25 +0800
tags: [git]
toc: true
math: false
---

![Git & Github](https://blog.kakaocdn.net/dn/obZjH/btqF3b8YFA8/m1c8xWYH0uAz7PVkt3q8M0/img.png)

## 깃을 배워야 하는 이유 ?

Git은 VCS <mark>(Version Control System)</mark>이라고 불리는 버전 관리 툴중에 하나이다.
이 깃이라는 것을 사용하게 된다면 필요에 따라 프로젝트의 시간과 차원을 관리할 수 있는 마치 닥터스트레인지의 타임스톤과 같은 힘을 가질 수 있게 된다.

### 프로젝트의 시간을 관리

혹시라도 실무나 개인 프로젝트에서 저장한 버전들이 1번에서 5번까지 있다고 치자. 이 버전들을 계속해서 실행해 나가다가 3번부터 5번까지의 버전에서는 문제가 없었지만 2번 버전에서는 오류가 발생하였다고 가정을 하자면 이는 매우 곤란할 것이다.

깃을 쓰지 않고 하는 방법도 있겠지만 매번 각 버전의 파일들을 저장하여 보존하려면 매우 큰 용량을 차지해나갈 것이기도 하며 관리하기도 매우 까다롭다. 만약에 깃을 사용하게 된다면 커밋메세지를 통해서 각 버전들의 디테일한 시점까지 돌아갈 수 있다.

### 프로젝트의 차원을 관리

Git으로는 차원여행 즉 멀티버스같은 차원 이동이 가능하다. 혹시나 팀 프로젝트를 진행중에 새로운 시도를 해보고 싶은데 개인 프로젝트가 아니라서 이를 함부로 만져볼 수 없거나, 팀 내부에서 다양한 시도들을 하려고 하고 만약에 내가 한 시도가 너무 좋아서 메인 프로젝트로 가지고 오고 싶다고 어떻게 할 것인가? 이마저도 Git으로는 충분히 브런치라는 차원들을 통해 옮겨 다니면서 작업을 할 수 있다.

깃은 여러 개발자들이 협업해서 만드는데 매우 중요하고 규모의 프로젝트를 수행하는데 있어서 없어서는 안될 툴이므로 꼭 배워두는 것이 좋다.

---

## Git 설치 및 환경세팅

<br>

### Git Version Check

```
git --version
```

협업시 윈도우와 맥에서 엔터 방식 차이로 인한 오류를 방지

```
git config --global core.autocrlf input
```

### Git Download by HomeBrew

```
brew install git
```

### GUI Download

[SourceTree](https://www.sourcetreeapp.com)

[GitHub Desktop, GitKraken 등](https://git-scm.com/downloads/guis)

### Iterm2 Install & Setting

[Iterm2](https://iterm2.com)

### CLI vs GUI

CLI : Command Line Interface

GUI : Graphical User Interface

---

## Git 최초 설정

<br>

Git global로 사용자 이름과 이메일 설정

```
git config --global user.name "(본인 이름)"
git config --global user.email "(본인 이메일)"
```

확인하기

```
git config --global user.name
git config --global user.email
```

기본 브랜치명 변경

```
git config --global init.defaultBranch main
```

### 프로젝트 생성 & Git 관리 시작

```
git init
```

터미널에서 해당 파일에 이를 실행하게 된다면 숨김모드로 .git 폴더가 생성된다

---

## .gitignore 관리하기

### .gitignore가 필요한 경우

- 포함할 필요가 없을 때 : 자동으로 생성 또는 다운로드되는 파일(빌드 결과물, 라이브러리)

- 포함하지 말아야 할 때 : 보안상 민감한 정보를 담은 파일

이럴때는 .gitignore을 사용하여 배제시켜버릴 수 있다.

<br>

### .gitignore 형식

[.gitignore 참조사이트](https://git-scm.com/docs/gitignore)

```
# 이렇게 #를 사용해서 주석

# 모든 file.c
file.c

# 최상위 폴더의 file.c
/file.c

# 모든 .c 확장자 파일
*.c

# .c 확장자지만 무시하지 않을 파일
!not_ignore_this.c

# logs란 이름의 파일 또는 폴더와 그 내용들
logs

# logs란 이름의 폴더와 그 내용들
logs/

# logs 폴더 바로 안의 debug.log와 .c 파일들
logs/debug.log
logs/*.c

# logs 폴더 바로 안, 또는 그 안의 다른 폴더(들) 안의 debug.log
logs/**/debug.log
```

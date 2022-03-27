---
layout: post
title: 제대로 파는 Git & Github 9 🐙
date: 2022-03-27 14:00 +0800
# last_modified_at: 2022-02-16 01:08:25 +0800
tags: [git]
toc: true
math: false
---

![Git & Github](https://blog.kakaocdn.net/dn/obZjH/btqF3b8YFA8/m1c8xWYH0uAz7PVkt3q8M0/img.png)

# Git의 추가 기능들

## 🎣 Git Hooks

Git상의 이벤트마다 자동으로 실행될 스크립트를 지정합니다.

📁 Git Hooks 폴더 보기

프로젝트 폴더 내 .git > hooks 폴더 확인

- 파일 끝에 .sample을 없애면 훅 실행파일이 됨

### gitmoji-cli로 활용예 보기

<a href="https://gitmoji.dev/">Gitmoji Website</a>

<mark>For Window</mark>

- 먼저 Node.js 설치
- 터미널에서 설치: npm i -g gitmoji-cli

<mark>For Mac</mark>

- brew로 설치 : brew install gitmoji

프로젝트의 훅에 적용
프로젝트 폴더에서 아래 명령어 실행

```
gitmoji -i
```

- hooks 폴더에 추가된 파일 확인하기
- 프로젝트에 수정 뒤 git add ., git commit하여 진행
- 커밋 추가 뒤 push하여 GitHub에서 확인

⛔ gitmoji-cli 훅을 해제하려면

hooks폴더에서 prepare-commit-msg 파일을 삭제해주면 됩니다.

---

## 📦️ Git Submodules

### 서브모듈

- 프로젝트 폴더 안에 또 다른 프로젝트가 포함될 때 사용
- 여러 프로젝트에 사용되는 공통모듈일 때 유용

![git-module-img](https://www.yalco.kr/images/lectures/git-github-dive/12-2/submodules.png)

### 두 개의 프로젝트 생성

- main-project, submodule
- 양쪽 모두 파일 생성 및 작성 뒤 커밋

- 두 프로젝트 모두 GiHub에 각각 레포지토리 만들어 올리기
  - 혹은 GitHub에서 생성해도 좋음

### <mark>main-project</mark>에 서브모듈로 <mark>submodule</mark> 프로젝트 추가

main-project 디렉토리상 터미널에서 아래 명령어 실행

```
git submodule add (submodule의 GitHub 레포지토리 주소) (하위폴더명, 없을 시 생략)
```

- 프로젝트 폴더 내 submodule폴더와 .gitmodules 파일 확인
- 스테이지된 변경사항 확인 뒤 커밋
- 양쪽 모두 수정사항 만든 뒤 main-project에서 git status로 확인

  - submodule의 변경사항은 포함되지 않음 확인

- main-project에서 변경사항 커밋 뒤 푸시
- submodule에서 변경사항 커밋 뒤 푸시
- main-project에서 상태 확인
- main-project에서 커밋, 푸시 뒤 GitHub에서 확인

### 서브모듈 업데이트

1. main-project 새로운 곳에 clone 하기
2. 아래 명령어들로 서브모듈 init 후 클론

```
git submodule init (특정 서브모듈 지정시 해당 이름)
```

```
git submodule update
```

3. GitHub에서 submodule에 수정사항 커밋

main-project에서 아래 명령어로 업데이트

```
git submodule update --remote
```

- 서브모듈 안에 또 서브모듈이 있을 시: --recursive 추가

---

---
layout: post
title: 제대로 파는 Git & Github 10 🐙
date: 2022-03-28 16:00 +0800
# last_modified_at: 2022-02-16 01:08:25 +0800
tags: [git]
toc: true
math: false
---

![Git & Github](https://blog.kakaocdn.net/dn/obZjH/btqF3b8YFA8/m1c8xWYH0uAz7PVkt3q8M0/img.png)

# GitHub 잘 사용하기

## 📦️ 프로젝트와 폴더에 대한 문서

README.md 파일을 작성하여서 프로젝트의 정보들을 나타내자!

홈페이지 참고

<a href="https://www.markdownguide.org/cheat-sheet/"><mark>Markdown Cheat Sheet</mark></a>

<a href="https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax">
<mark>GitHub Docs</mark></a>

---

## 🍻 풀 리퀘스트와 이슈

### Pull Request (PR)

기본적으로 setting 메뉴에 들어가서 Collaborators를 누르면 Manage access가 나온다. 여기에서 팀원들을 추가 할 수 있음

변경사항을 merge하기 전 리뷰를 거치기 위함

- 팀원들의 동의를 거친 뒤 대상 브랜치에 적용

폴 리퀘스트 사용해보기

1. 새로운 브랜치 생성 후 변경사항 커밋하여 푸쉬
2. GitHub 레포지토리 페이지에서 Compare & pull request 버튼 클릭

   - 또는 ~ branches에서 New pull request 클릭

3. 메시지 작성 후 Create pull request 클릭

풀 리퀘스트 검토 후 처리하기

1. GitHub 레포지토리 페이지에서 Pull requests 탭 클릭
2. 대상 풀 리퀘스트 클릭하여 내용 검토
   - 의견이 있을 시 코멘트 달기
   - 반려해야 할 시 Close pull request
   - 승인할 시 Merge pull request

### Issue

버그나 문제 제보, 추가할 기능 등의 이슈 소통

이슈 작성해보기

1. GitHub 레포지토리 페이지에서 Issues 탭 클릭
2. 필요시 label 또는 milestone 생성

   - milestone: 이슈의 주제 묶음 (특정 목표 등)

3. 이슈 작성

   - 필요시 label, milestone, asignee 지정

4. 이슈 확인 후 처리

   - 코멘트 달기
   - 관련 개발 착수 (브랜치명이나 커밋 footer에 이슈 번호 반영)
   - 해결 뒤: Close issue

---

## 오픈소스에 참여하기

오픈소스 프로젝트에 기여하기 === Contributors에 이름 올리기

⭐️ 프로젝트별 참여 가이드 확인

<a href="https://github.com/facebook/react">React GitHub</a>

1. 프로젝트 fork 해보기
   원하는 유명 프로젝트 내 레포지토리로 포크해보기

2. 코드 기여하기
   코드 수정 후 pull request

3. 오픈소스 주인 관점
   풀 리퀘스트 코멘트/반려/수락

---

## 🔑 SSH로 접속하기

SSH란 암호키와 공개키를 가지고 암호화된 정보들을 주고 받고 하는 기능이다.
처음 주어지는 암호키와 공개키를 가지고 서로 알고리즘을 풀어내 복호화가 가능하다. 이외의 공개키 혹은 암호키를 가지고는 절대로 풀 수 없다.

### SSH 프로토콜을 통한 인증

- 공개키 암호화 방식 활용
- username과 토큰 사용할 필요 없음
- 컴퓨터 자체에 키 저장

### SSH 키 등록하기

- 계정의 Settings - SSH and GPG keys
- 해당 페이지의 가이드 참조

이외 강의 참고

---

## 🗝 GPG로 커밋에 사인하기

### GPG 키를 통한 검증

GPG는 GnuPG = GNU Privacy Guard로 PGP(Preety Good Privacy)를 대체하는 암호화, 복호화 프로그램이다.

깃허브에서 가끔 커밋메시지 Verified라는 로고를 볼 수 있는데 이 경우는 2가지 이다.

1. Github 자체 홈페이지에서 수정 해서 커밋 할 경우
2. GPG 키를 받아 깃과 연동시킨 경우

💡 주로 회사에서나 큰 프로젝트 일 경우 사용됨

### GitHub 커밋 내역 살펴보기

- 로컬에서 푸시한 커밋과 GitHub에서 작성한 커밋 비교
- Verified : 신뢰할 만한 출처에서 커밋되었다는 인증

GPG 사용

1. GPG 툴 설치
   윈도우: 다운로드 사이트
   맥: brew install gnupg
   gpg --version으로 확인

이외는 강의 참조

---

## 💥 GitHub Action

GitHub Actions를 사용하면 이제 세계적 수준의 CI/CD로 모든 소프트웨어 워크플로를 쉽게 자동화할 수 있습니다. GitHub에서 바로 코드를 빌드, 테스트 및 배포하세요. 코드 검토, 분기 관리 및 문제 분류가 원하는 방식으로 작동하도록 합니다.

참고 용어
CI/CD : 지속적 통합과 배포

- CI

  - Continuous Integration
  - 테스트와 빌드를 자동으로 진행하는 프로세스

- CD

  - Continuous Deploy, Continuous Delivery
  - 배포 자동화

동종: GitLab CI/CD, BitBucket Pipelines

---

## 🐙 GitHub 추가 팁

### OctoTree

![Octotree](https://www.yalco.kr/images/lectures/git-github-dive/14-4/octotree.png)

- GitHub 레포지토리의 디렉토리를 보다 편하게 브라우징
- 크롬 익스텐션 (엣지에서 사용 가능)

### GitHub CLI

- GitHub 작업 전용 CLI 툴

<a href="https://cli.github.com/">GitHub CLI Docs</a>

<a href="https://cli.github.com/">GitHub 주요 명령어 </a>

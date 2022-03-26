---
layout: post
title: 제대로 파는 Git & Github 8 🐙
date: 2022-03-26 14:00 +0800
# last_modified_at: 2022-02-16 01:08:25 +0800
tags: [git]
toc: true
math: false
---

![Git & Github](https://blog.kakaocdn.net/dn/obZjH/btqF3b8YFA8/m1c8xWYH0uAz7PVkt3q8M0/img.png)

# Branch 보다 깊이 알기

## 🐰 Fastforward vs 3-way merge

### ⭐ Fastforward

메인 브랜치에서는 아무런 변화가 없고, 다른 브랜치에서는 변화가 있을 때 그 브랜치와 merge 하는 과정에서는 굳이 메인 브랜치에서 따로 하나의 커밋을 만들어서 그 브랜치와 merge 할 이유가 없기에 그 브랜치의 끝 커밋을 그냥 main 브랜치로 만드는 과정

### ⭐ 3-way merge

Fastforward와는 다르게 메인과 타 브런치에서의 최소 하나 이상의 커밋을 할 경우 그 브랜치를 메인 브랜치로 끌고와 둘이 병합하는 과정이다.

---

## 다른 브랜치에서 원하는 🍒 커밋만 따오기

![cherryPick](https://www.yalco.kr/images/lectures/git-github-dive/10-2/branches.png)

### 다른 브랜치의 원하는 커밋 가져오기

cherry-pick

🎯 Cherry 커밋 main 브랜치로 가져오기

main 브랜치에서 실행

```
git cherry-pick (체리의 해시)
```

💡 fruit 브랜치의 Cherry와는 별개의 커밋

---

## 다른 가지의 🌿 잔가지만 가져오기

다른 브랜치에서 파생된 브랜치 옮겨붙이기

rebase --onto 옵션 사용

🎯 fruit 브랜치에서 파생된 citrus 브랜치를 main 브랜치로 옮겨붙이기

```
git rebase --onto (도착 브랜치) (출발 브랜치) (이동할 브랜치)
```

- git rebase --onto main fruit citrus
- citrus로 fast forward

---

## 다른 가지의 마디들 🗜️ 묶어서 가져오기

다른 커밋들을 하나로 묶어 가져오기

merge --squash 옵션 사용

🎯 root 브랜치의 마디들을 하나로 묶어 main 브랜치로 가져오기

```
git merge --squash (대상 브랜치)
```

- 변경사항들 스테이지 되어 있음
- git commit 후 메시지 입력

⚠️ 일반 merge와의 차이 정리

일반 merge와 merge --squash는, 실행 후 코드의 상태는 같지만
내역 면에서 큰 차이가 있는 것이라고 이해하시면 됩니다.

- 일반 merge : A와 B 두 브랜치를 한 곳으로 이어붙임
- merge --squash : B 브랜치의 마디들을 복사해다가 한 마디로 모아 A 브랜치에 붙임 (staged 상태로)

---

## ⭐⭐⭐ 협업을 위한 브랜치 활용법 (Gitflow)

협업을 위한 브랜칭 전략

https://nvie.com/posts/a-successful-git-branching-model/
위 페이지의 도표 참조

### 사용되는 브랜치들

브랜치 | 용도
main | 제품 출시/배포
develop | 다음 출시/배포를 위한 개발 진행
release | 출시/배포 전 테스트 진행(QA)
feature | 기능 개발
hotfix | 긴급한 버그 수정

---

# 분석하고 디버깅하기

## 🏷️ log 더 자세히 알아보기

### 옵션들을 활용한 다양한 사용법

⭐ 각 커밋마다의 변경사항 함께 보기

```
git log -p
```

⭐ 최근 n개 커밋만 보기

```
git log -(갯수)
```

⭐ 통계와 함께 보기

```
git log --stat
더 간략히: --shortstat
```

⭐ 한 줄로 보기

```
git log --oneline
```

⭐ 변경사항 내 단어검색

```
git log -S (검색어)
```

- George로 검색

⭐ 커밋 메시지로 검색

```
git log --grep (검색어)
```

⭐ 자주 사용되는 그래프 로그 보기

```
git log --all --decorate --oneline --graph
```

- --all : 모든 브랜치 보기
- --graph : 그래프 표현
- --decorate : 브랜치, 태그 등 모든 레퍼런스 표시
  - --decorate=no
  - --decorate=short : 기본
  - --decorate=full

### ⭐⭐ 포맷된 로그 보기

얄코 커스텀 포맷

```
git log --graph --all --pretty=format:'%C(yellow) %h  %C(reset)%C(blue)%ad%C(reset) : %C(white)%s %C(bold green)-- %an%C(reset) %C(bold red)%d%C(reset)' --date=short
```

- date를 relative로 바꾸면 현재 기준 몇 일전이 나온다.
- 단축키로 등록하여 사용

---

## 차이 살펴보기

git diff : 워킹 디렉토리의 변경사항 확인

```
git diff
```

파일명만 확인

```
git diff --name-only
```

스테이지의 확인

```
git diff --staged
```

--cached와 같음

브랜치간의 차이 확인

```
git diff (브랜치1) (브랜치2)
```

---

## 누가 코딩했는지 알아내기

git blame : 각 라인의 작성자를 확인

파일의 부분별로 작성자 확인하기

```
git blame (파일명)
```

특정 부분 지정해서 작성자 확인하기

```
git blame -L (시작줄) (끝줄, 또는 +줄수) (파일명)
```

⭐️ VS Code의 GitLens 확장 사용해보기

---

## 오류가 발생한 시점 찾아내기

git bisect : 이진 탐색 알고리즘으로 문제의 발생 시점을 찾아냅니다.

🎯 v3 시점이 의심되는 상황

이진 탐색 시작

```
git bisect start
```

오류발생 지점임을 표시

```
git bisect start
```

의심 지점으로 이동

```
git checkout (해당 커밋 해시)
```

오류 발생 않을 시 양호함 표시

```
git bisect good
```

♻️ 원인을 찾을 때까지 반복

```
git bisect good/bad
```

이진 탐색 종료

```
git bisect reset
```

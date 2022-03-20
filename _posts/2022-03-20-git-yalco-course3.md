---
layout: post
title: 제대로 파는 Git & Github 3 🐙
date: 2022-03-20 11:00 +0800
# last_modified_at: 2022-02-16 01:08:25 +0800
tags: [git]
toc: true
math: false
---

![Git & Github](https://blog.kakaocdn.net/dn/obZjH/btqF3b8YFA8/m1c8xWYH0uAz7PVkt3q8M0/img.png)

# 차원 넘나들기 🚪

## 🌳 여러 branch 만들어보기

Branch: 분기된 가지 (다른 차원)

- 프로젝트를 하나 이상의 모습으로 관리해야 할 때

<mark>예) 실배포용, 테스트서버용, 새로운 시도용</mark>

- 여러 작업들이 각각 독립되어 진행될 때

<mark>예) 신기능 1, 신기능 2, 코드개선, 긴급수정...
각각의 차원에서 작업한 뒤 확정된 것을 메인 차원에 통합</mark>

브렌치의 주요 목적은 분업이다. 어느 정도 규모의 프로젝트가 진행되면 절대 그 프로젝트는 혼자 하기에는 너무 오랜 시간이 걸린다. 이로 인해 매번 다른 배포를 해나가면서, 배포 버전마다 각기 다른 기능들이 있기에 이를 테스트 해보고 디버깅을 해나가면서 좋은 버전은 메인 브렌치에 merge 시키고 다시 배포하는 그런 git-flow 전략을 사용할 수 있다.

![Git branch](https://www.yalco.kr/images/lectures/git-github/3-1/branches.png)

### 브랜치 생성 / 이동 / 삭제하기

add-coach란 이름의 브랜치 생성

```
git branch add-coach
```

브랜치 목록 확인

```
git branch
```

add-coach 브런치로 이동

```
git switch add-coach
```

<mark>checkout 명령어가 Git 2.23 버전부터 switch, restore로 분리</mark>

💡 브랜치 생성과 동시에 이동하기

```
git switch -c new-teams
```

기존의 git checkout -b (새 브랜치명)

🗑 브랜치 삭제하기

```
git branch -d (삭제할 브랜치명)
```

to-delete란 브랜치 만들고 삭제해보기

<mark> 지울 브랜치에 다른 브랜치로 적용되지 않은 내용의 커밋이 있을 시에는 -D(대문자) 옵션으로 강제 삭제합니다.</mark>

```
git branch -D(브랜치명)
```

✏️ 브랜치 이름 바꾸기

```
git branch -m (기존 브랜치명) (새 브랜치명)
```

---

### 각각의 브랜치에서 서로 다른 작업해보기(실습)

Yalco 홈페이지 참고

### 결과 살펴보기

각자 다른 브랜치에서 git log를 사용해보면 각 브런치마다 로그가 다르게 되어있는것을 볼 수 있다. 이는 add, commit이 해당 브런치에서만 영향을 끼칠 수 있다는 것을 알 수 있다.

소스트리 말고도 CLI 에서도 여러 브랜치를 시각화 해서 볼 수 있다.

```
git log --all --decorate --oneline --graph
```

![Example](https://mackyle.github.io/git-log-compact/image1.gif)

---

## 🐰 branch를 합치는 두 가지 방법

서로 다른 브랜치를 합치는 두 방식

<mark>merge : 두 브랜치를 한 커밋에 이어붙입니다.</mark>

브랜치 사용내역을 남길 필요가 있을 때 적합한 방식입니다.
다른 형태의 merge에 대해서도 이후 다루게 될 것입니다.

<mark>rebase : 브랜치를 다른 브랜치에 이어붙입니다.</mark>

한 줄로 깔끔히 정리된 내역을 유지하기 원할 때 적합합니다.
이미 팀원과 공유된 커밋들에 대해서는 사용하지 않는 것이 좋습니다.

## 🎲 branch 합치기 실습

### merge로 합치기

add-coach 브랜치를 main 브랜치로 merge

- main 브랜치로 이동
- 아래의 명령어로 병합

```
git merge add-coach
```

- :wq로 자동입력된 커밋 메시지 저장하여 마무리
- 소스트리에서 확인

💡 merge는 reset으로 되돌리기 가능

- merge도 하나의 커밋
- merge하기 전 해당 브랜치의 마지막 시점으로

❗ 병합된 브랜치는 삭제

삭제 전 소스트리에서 add-coach 위치 확인

```
git branch -d add-coach
```

---

### rebase로 합치기

new-teams 브랜치를 main 브랜치로 rebase

- new-teams 브랜치로 이동

🛑 merge때와는 반대! 이동할 해당 브랜치로 이동해서 기존 main 브랜치로 rebase 시도

- 아래의 명령어로 병합

```
git rebase main
```

- 소스트리에서 상태확인 : 현재 main 브랜치는 rebased 된 브랜치보다 뒤쳐져 있는 상황

- main 브랜치로 이동 후 아래 명령어로 new-teams의 시점으로 fast-forward

```
git merge new-teams
```

- new-teams 브랜치는 삭제하도록 한다.

```
git branch -d new-teams
```

---

## 🧨 충돌 해결하기

만약에 다른 두 개발자가 같은 위치에 다른 내용을 수정하고 merge할 경우에는 충돌하게 되는데 이를 해결해보자!

### 브랜치 간 충돌

홈페이지 참조 및 실습 진행

### merge 충돌 해결하기

git merge conflict-1로 병합을 시도하면 충돌 발생

- 오류 메시지와 git status 확인
- VS Code에서 해당 부분 확인

❗ 너무 많은 부분들이 충돌하여 당장 해결이 어려울 경우 아래 명령어로 merge 중단

```
git merge --abort
```

❗ 해결 가능 시
충돌 부분을 수정한 뒤 git add ., git commit으로 병합 완료

### rebase 충돌 해결하기

conflict-2에서 git rebase main로 리베이스 시도하면 충돌 발생

- 오류 메시지와 git status 확인
- VS Code에서 해당 부분 확인

❗ 방금 merge와 같이 상황에서 당장 충돌 해결이 어려울 경우 아래 명령어로 rebase 중단

```
git rebase --abort
```

❗ 해결 가능 시

- 충돌 부분을 수정한 뒤 git add .
- 아래 명령어로 계속

```
git rebase --continue
```

- 충돌이 모두 해결될 때까지 반복

그리고 난 뒤

❗ main에서 git merge conflict-2로 마무리 (꼭 merge를 해줘야지 됨 안그러면 main 브랜치는 rebase된 브랜치보다 뒤쳐져 있게 됨)

이후 conflict-1 , conflict-2로 브랜치 삭제

```
git branch -d conflict-1
git branch -d conflict-2
```

---

---
layout: post
title: 제대로 파는 Git & Github 5 🐙
date: 2022-03-22 14:00 +0800
# last_modified_at: 2022-02-16 01:08:25 +0800
tags: [git]
toc: true
math: false
---

![Git & Github](https://blog.kakaocdn.net/dn/obZjH/btqF3b8YFA8/m1c8xWYH0uAz7PVkt3q8M0/img.png)

# Git 보다 깊이 알기

## 🐰 Git을 특별하게 만드는 것

실습 ❌

1. Snapshot
2. 분산 버전 관리

## Git의 3가지 공간

![git-workspace](https://www.yalco.kr/images/lectures/git-github-dive/5-2/three2.png)

🍱 Working directory

- untracked: Add된 적 없는 파일, ignore 된 파일
- tracked: Add된 적 있고 변경내역이 있는 파일
- git add 명령어로 Staging area로 이동

🍱 Staging area

- 커밋을 위한 준비 단계
  - 예시: 작업을 위해 선택된 파일들
- git commit 명령어로 repository로 이동

🍱 Repository

- .git directory라고도 불림
- 커밋된 상태

---

### 파일의 삭제와 이동

파일 삭제

```
git rm
```

파일 이동

```
git mv
```

파일을 staging area에서 working directory로

```
git restore --staged (파일명)
```

- --staged를 빼면 working directory에서도 제거
- 예전: git reset HEAD (파일명)

---

### reset의 세 가지 옵션

- --soft: repository에서 staging area로 이동
- --mixed (default): repository에서 working directory로 이동
- --hard: 수정사항 완전히 삭제

---

## 🪦 HEAD : HEAD라는 가상 branch 상태 사용해보기

![git-head](https://www.yalco.kr/images/lectures/git-github-dive/5-3/heads.png)

Git의 HEAD
<mark>현재 속한 브랜치의 가장 최신 커밋</mark>

- switch로 브랜치 이동해보기
  - main과 delta-branch

checkout으로 앞뒤 이동해보기

```
git checkout HEAD^
```

- ^ 또는 ~ 갯수만큼 이전으로 이동

```
git checkout HEAD^^^, git checkout HEAD~4
```

- ⭐️ 커밋 해시를 사용해서도 이동 가능

```
git checkout (커밋해시)
```

- (이동을) 한 단계 되돌리기

```
git checkout -
```

💡 이전으로 checkout된 상태에서 소스트리로 HEAD 상태 보기

익명의 브랜치에 위치함을 알 수 있음

- checkout 으로 이전으로 돌아간 뒤
  - 기존 브랜치로 돌아오기 : git switch (브랜치명)
  - 새 브랜치 만들어보기
  - 새 커밋 만들어보기

⭐ HEAD 사용하여 reset하기

```
git reset HEAD(원하는 단계) (옵션)
```

---

## fetch vs pull

⭐ fetch 와 pull 차이

- fetch: 원격 저장소의 최신 커밋을 로컬로 가져오기만 함
- pull: 원격 저장소의 최신 커밋을 로컬로 가져와 merge 또는 rebase

fetch한 내역 적용 전 살펴보기

1. 원격의 main 브랜치에 커밋 추가

- git checkout origin/main으로 확인해보기

2. 원격의 변경사항 fetch

- git checkout origin/main으로 확인해보기
- pull로 적용

### 원격의 새 브랜치 확인

```
git checkout origin/(브랜치명)
git switch -t origin/(브랜치명)
```

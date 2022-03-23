---
layout: post
title: 제대로 파는 Git & Github 6 🐙
date: 2022-03-23 22:00 +0800
# last_modified_at: 2022-02-16 01:08:25 +0800
tags: [git]
toc: true
math: false
---

![Git & Github](https://blog.kakaocdn.net/dn/obZjH/btqF3b8YFA8/m1c8xWYH0uAz7PVkt3q8M0/img.png)

# Git 보다 잘 활용하기

## 🔖 Help와 문서 활용하기

Git 사용 중 잘 모르는 부분이 있을 때 도움을 받을 수 있는 기능

```
git help
```

- 기본적인 명령어들과 설명

```
git help -a
```

- Git의 모든 명령어들
- j로 내리기, k로 올리기, :q로 닫기

```
git (명령어) -h
```

- 해당 명령어의 설명과 옵션 보기

```
git help (명령어)
```

```
git (명령어) --help
```

- 해당 명령어의 설명과 옵션 웹사이트에서 보기
  ⭐️ 웹에서 열리지 않을 시 끝에 -w를 붙여 명시

### 📎 Git 문서 Url

https://git-scm.com/docs

### 📚 Git Book Url

https://git-scm.com/book/ko/v2

---

## 🔨Git의 각종 설정

### global 설정과 local 설정

config를 --global과 함께 지정하면 전역으로 설정됩니다.

- 특정 프로젝트만의 user.name과 user.email 지정해보기

### 설정값 확인

현재 모든 설정값 보기

```
git config (global) --list
```

에디터에서 보기 (기본: vi)

```
git config (global) -e
```

기본 에디터 수정

```
git config --global core.editor "code --wait"
```

- 또는 code 자리에 원하는 편집 프로그램의 .exe파일 경로 연결
- --wait : 에디터에서 수정하는 동안 CLI를 정지
- 💡 git commit 등의 편집도 지정된 에디터에서 열게 됨

❗ 위의 에디터 설정을 되돌리려면

git config --global -e로 편집기를 연 뒤 아래 부분을 삭제하고 저장

⭐️ 맥에서 code로 VS Code가 실행되지 않을 시

- VS Code에서 command + shift + p
- shell로 검색하여 셸 명령: PATH에 code 명령 설치 선택

- 영문: Shell Command: Install 'code' command in PATH

### 유용한 설정들

줄바꿈 호환 문제 해결

```
git config --global core.autocrlf (윈도우: true / 맥: input)
```

pull 기본 전략 merge 또는 rebase로 설정

```
git config pull.rebase false
git config pull.rebase true
```

기본 브랜치명

```
git config --global init.defaultBranch main
```

push시 로컬과 동일한 브랜치명으로

```
git config --global push.default current
```

### 단축키 설정

```
git config --global alias.(단축키) "명령어"
예시: git config --global alias.cam "commit -am"
```

---

# 프로답게 커밋 관리하기

## 🐰 어떻게 커밋하는게 좋을까요?

### 작업을 커밋할 때 권장사항 (Git Flow)

1. 하나의 커밋에는 한 단위의 작업을 넣도록 합니다.
   - 한 작업을 여러 버전에 걸쳐 커밋하지 않습니다.
   - 여러 작업을 한 버전에 커밋하지 않습니다.
2. 커밋 메시지는 어떤 작업이 이뤄졌는지 알아볼 수 있도록 작성합니다.

### ⭐ 커밋 메시지 컨벤션

널리 사용되는 커밋 메시지 작성방식

```
type: subject

body (optional)
...
...
...

footer (optional)
```

예시 :

```
feat: 압축파일 미리보기 기능 추가

사용자의 편의를 위해 압축을 풀기 전에
다음과 같이 압축파일 미리보기를 할 수 있도록 함
 - 마우스 오른쪽 클릭
 - 윈도우 탐색기 또는 맥 파인더의 미리보기 창

Closes #125
```

⭐ <mark>커밋 메세지 타입</mark>

```
feat : 새로운 기능 추가
fix : 버그 수정
docs : 문서 수정
style : 공백, 세미콜론 등 스타일 수정
refactor : 코드 리팩토링
perf : 성능 개선
test : 테스트 추가
chore : 빌드 과정 또는 보조 기능(문서 생성기능 등) 수정
```

⭐ Subject
커밋의 작업 내용 간략히 설명

⭐ Body
길게 설명할 필요가 있을 시 작성

⭐ Footer
Breaking Point 가 있을 때
특정 이슈에 대한 해결 작업일 때

Git imoji 관련 사이트 : https://gitmoji.dev/

---

### 보다 세심하게 스테이징하고 커밋하기

아래 명령어로 hunk별 스테이징 진행

- 옵션 설명을 보려면 ?입력 후 엔터
- y 또는 n로 각 헝크 선택
- 일부만 스테이징하고 진행해보기
- git stats와 소스트리로 확인

### 변경사항을 확인하고 커밋하기

```
git commit -v
```

- j, k로 스크롤하며 내용 확인
- git diff --staged와 비교
- 커밋 후 남은 헝크를 다른 버전으로 커밋해보기

### 커밋하기 애매한 변화 치워두기

### 변경사항 만들기

- Tigers의 members에 Stash 추가
- tomcats.yaml 추가 후 add

```
team: Tomcats

coach: Apache
```

### 아래 명령어로 치워두기

```
git stash
```

- git stash save와 같음

### 원하는 시점, 브랜치에서 다시 적용

```
git stash pop
```

### 원하는 것만 stash 해보기

- Leopards의 members에 Stash2 추가
- Jaguars의 members에 Stash3 추가
- 아래 명령어로 Stash2만 선택하여 스태시

```
git stash -p
```

### 메시지와 함께 stash

```
git stash -m 'Add Stash3'
```

### stash 목록 보기

```
git stash list
```

- 리스트상의 번호로 apply, drop, pop 가능
  - ex) git stash apply stash@{1}

### Stash 사용법 정리

명령어 | 설명 | 비고
git stash | 현 작업들 치워두기 | 끝에 save 생략
git stash apply | 치워둔 마지막 항목(번호 없을 시) 적용 |끝에 번호로 항목 지정 가능
git stash drop | 치워둔 마지막 항목(번호 없을 시) 삭제 |끝에 번호로 항목 지정 가능
git stash pop | 치워둔 마지막 항목(번호 없을 시) 적용 및 삭제 | apply + drop
git stash branch | (브랜치명) 새 브랜치를 생성하여 pop | 충돌사항이 있는 상황 등에 유용
git stash clear | 치워둔 모든 항목들 비우기

---

## 🛠 커밋 수정하기

마지막 커밋 메세지 수정

```
git commit --amend
```

### 커밋 메시지 변경

- Panthers의 members에 Hoki 추가하고 스테이지
- 커밋 메시지: 횻홍
- 아래 명령어로 에디터 열어 커밋 메시지 변경

```
git commit --amend
```

- 커밋 메시지: Add a member to Panthers

### 커밋에 변화 추가

- Pumas의 members에 Poki 추가하고 스테이지
- git commit --amend로 마지막 커밋에 포함
- 커밋 메시지 아무렇게나 변경

### ⭐ 커밋 메시지 한 줄로 변경

```
git commit --amend -m 'Add members to Panthers and Pumas'
```

---

## 🧰 과거의 커밋들을 수정, 삭제, 병합, 분할하기

git rebase -i (대상 바로 이전 커밋)

- 과거 커밋 내역을 다양한 방법으로 수정 가능

p, pick : 커밋 그대로 두기
r, reword : 커밋 메시지 변경
e, edit : 수정을 위해 정지
d, drop : 커밋 삭제
s, squash : 이전 커밋에 합치기

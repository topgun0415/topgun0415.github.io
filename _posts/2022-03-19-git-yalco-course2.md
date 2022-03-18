---
layout: post
title: 제대로 파는 Git & Github 2 🐙
date: 2022-03-19 01:00 +0800
# last_modified_at: 2022-02-16 01:08:25 +0800
tags: [git]
toc: true
math: false
---

![Git & Github](https://blog.kakaocdn.net/dn/obZjH/btqF3b8YFA8/m1c8xWYH0uAz7PVkt3q8M0/img.png)

# 시간 여행하기 🕰️

## 💊 변화를 타임캡슐에 담아 묻기

### 프로젝트의 변경사항들을 타임캡슐(버전)에 담기

vscode에서 저장이나 어떠한 상태가 변경되었을 때 초록색으로 파일이 나타날 것이고 이를 확인해 보기 위해서는 git status 라는 것을 입력한다.

```
git status
```

혹시나 파일 옆에 U나 터미널 상에 ?? 라고 뜨는 것은 추적하지 않는(untracked) 파일 즉 Git의 관리에 들어간 적 없는 파일이다.

그러면 파일을 하나 타임캡슐에 담아보자 !

```
git add tigers.yaml
```

git status로 다시 보면 tigers 파일이 A로 나오는 것을 볼 수 있다. 이것은 추적되고 있다는 뜻이다. 그러면 모든 파일을 담아보자 !

```
git add .
```

git status로 확인해보면 모든 파일이 A로 변하는 것을 볼 수 있다. 하지만 이는 commit의 메세지를 따로따로 넣어줘야하는 이유로 인해서 상황을 보면서 사용하면 된다.

---

### 타임캡슐 묻기

담았던 파일들을 이제 묻어보자! 묻는 단축키는 commit

```
git commit
```

커밋을 할때 단순하게 git commit 이라는 단축키만은 잘 쓰이지 않겠지만 이를 입력하게 된다면 <mark>Vi 입력모드</mark>로 전환되게 된다.

Vi 입력모드 간단한 단축키는

- 입력시작 : i
- 입력종료 : ESC
- 저장 없이 종료 : q
- 저장없이 강제종료 : q!
- 저장하고 종료 : wq
- 위로 스크롤 : k
- 아래로 스크롤 : j

하여튼 위와 같은 git commit 말고 실제로 많이 쓰이는 커밋 단축키가 있다.

```
git commit -m "FIRST COMMIT"
```

그리고 이를 확인하기 위해서는

```
git log
```

종료는 q로 끝낸다.

---

### 다음 변경사항들을 만들고 타임캡슐에 묻기

아래와 같은 변경사항들을 만들고 저장해본다.

- lions.yaml 파일 삭제
- tigers.yaml의 manager를 Donald로 변경
- leopards.yaml 파일 추가

```
team: Leopards

manager: Luke

members:
- Linda
- William
- David
```

git status로 확인 혹은 git diff로도 확인 가능함

그리고 캡슐에 담아보자

```
git add .
```

git status로 확인하면 변경된 사항들은 M으로 노란색으로 그리고 새로 만들어진 Leopards는 초록색으로 나올 것이다.

```
git commit -m "Replace Lions with Leopards
```

<mark> Tip : add와 commit 한꺼번에 하기 위해서는 </mark>

```
git commit -am "(메시지)"
```

🛑 새로 추가된(untracked) 파일이 없을 때 한정

---

## 🐰 과거로 돌아가는 두 가지 방법

Git에서 과거로 돌아가는 두 방식

- reset : 원하는 시점으로 돌아간 뒤 이후 내역들을 지웁니다.

- revert : 되돌리기 원하는 시점의 커밋을 거꾸로 실행합니다. 다만 revert로 돌아갔을 경우 전 log에는 방금 전 시점(되돌아가려 마음먹은 그 시점)이 존재한다.

<mark> 협업시 reset을 사용하게 된다면 해당 소스코드를 가지고 만들었던 다양한 사람들의 코드가 무효화되버릴 수 있으니 특이한 점이 있지않는 한 revert 사용 </mark>

---

## ⏲️ 과거로 돌아가기 실습

### reset 사용해서 과거로 돌아가기

아래 명령어로 커밋 내역 확인

```
git log
```

log를 보게된다면 commit 메세지에 Add team Cheetas의 커밋 해시가 보이게 된다

```
218d998b0b68f0d2b7c500227a7a250400a1c2bc
```

이를 복사하여서 reset에 붙여준다. <mark>최소 6자리정도 복사하는것을 추천</mark>

```
git reset --hard (돌아갈 커밋 해시)
```

---

### reset 하기 전 시점으로 복원해보기

백업해 둔 .git 폴더 사용

- .git 폴더 복원
- git log, git status로 상태 확인
- 아래 명령어로 현 커밋 상태로 초기화

```
git reset --hard
```

- 💡 뒤에 커밋 해시가 없으면 마지막 커밋으로 돌아가게 된다.
- lions.yaml 삭제

<mark>이는 실습을 위해 .git 폴더를 건드렸으나 실무에서는 .git 폴더를 건들여서 어떠한 일이 벌어질지 모르기 때문에 건드는 것을 삼가해야함</mark>

---

### revert로 과거의 커밋 되돌리기

Add George to Tigers의 커밋 해시 구하기

```
git revert (되돌릴 커밋 해시)
```

:wq로 커밋 메시지 저장

---

🎯 Replace Lions with Leopards의 커밋 되돌려보기

- 이후 leopards.yaml 수정한 내역 때문에 충돌

- git rm leopards.yaml로 Git에서 해당 파일 삭제
- git revert --continue로 마무리
- :wq로 커밋 메시지 저장

🎯 reset 사용해서 revert 전으로 되돌아가기

💡 커밋해버리지 않고 revert하기

```
git revert --no-commit (되돌릴  커밋 해시)
```

- 원하는 다른 작업을 추가한 다음 함께 커밋
- 취소하려면 git reset --hard

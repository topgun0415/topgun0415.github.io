---
layout: post
title: 보일러 플레이트(Boilerplate)란?
date: 2022-02-28 18:00 +0800
# last_modified_at: 2022-02-16 01:08:25 +0800
tags: [boilerplate]
toc: true
math: false
---

![Boilerplate](https://c8.alamy.com/comp/C216T5/steam-locomotive-boiler-under-repair-with-fire-tubes-removed-and-front-C216T5.jpg)

## 보일러 플레이트(Boilerplate)란?

<mark>보일러 플레이트</mark>란 보일러의 골격을 찍어내는 플레이트를 말한다. 즉 어떠한 형식의 틀을 만들어 놓고 변함없이 사용하는 것이다. 이렇게 똑같은 형태로 나온 골격에서 추가로 미세하게 더해서 상품을 내놓거나 하여 동일한 상품의 상품성을 유지해주고 만드는데 들어가는 시간을 단축시켜준다.

하나의 예시를 들자면. 전세를 구하기 위해서 부동산에 찾아갔고 마침 좋은 매물이 있다. 이 매물을 계약하기 위해 우리는 부동산 계약을 하기 위해 5장의 긴 분량의 매매계약서를 받았다. 하지만 계약서의 대부분은 같고, 약간의 세부적인 내용만 수정되어있다. 이것이 <mark>보일러 플레이트</mark>인 것이다!

이처럼 우리는 코드를 짜며 흔히 <mark>보일러 플레이트</mark>를 마주친 경험이 있을 것이다. 예를 들어 Vscode에서 Html 파일을 열고 느낌표(!) 하나면 이러한 코드를 만날 수 있다.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body></body>
</html>
```

리액트에서도 마찬가지로 create-react-app을 시작하면 자동으로 모듈 패키지가 설치되면서 개발자는 그저 코딩에만 신경쓰면 된다. 만약 cra가 없었다면 입문 리액트 개발자는 개봘환경만 세팅하다가 지루함을 느껴 금방 지쳐버리게 될 것이다.

![create-react-app](https://miro.medium.com/max/696/0*-hl5tR5sBHW-ME7d)

> 보일러 플레이트를 요약하자면 최소한의 수정 혹은 수정 없이 여러번 재사용 하는 것을 의미한다. 이러한 재사용은 개발자들의 편리성을 가져다주고 개발에만 집중할 수 있는 환경을 만들어준다.

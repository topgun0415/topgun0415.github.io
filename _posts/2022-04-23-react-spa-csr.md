---
layout: post
title: React SPA & CSR โ๏ธ
date: 2022-04-23 14:00 +0800
# last_modified_at: 2022-02-16 01:08:25 +0800
tags: [react]
toc: true
math: false
---

![React](https://ms314006.github.io/static/b7a8f321b0bbc07ca9b9d22a7a505ed5/97b31/React.jpg)

## ๐ก ๋ผ์ฐํ์ด๋ ๋ฌด์์ผ๊น ?

<mark>์ด๋ค ๋คํธ์ํฌ ๋ด์์ ํต์  ๋ฐ์ดํฐ๋ฅผ ๋ณด๋ผ ๊ฒฝ๋ก๋ฅผ ์ ํํ๋ ์ผ๋ จ์ ๊ณผ์ </mark>

ROUTER : ๋ฐ์ดํฐ์ ๊ฒฝ๋ก๋ฅผ ์ค์๊ฐ์ผ๋ก ์ง์ ํด์ฃผ๋ ์ญํ ์ ํ๋ ๋ฌด์ธ๊ฐ

ROUTING : ๊ฒฝ๋ก๋ฅผ ์ ํด์ฃผ๋ ํ์ ์์ฒด์ ๊ทธ๋ฐ ๊ณผ์ ๋ค์ ๋ค ํฌํจํ์ฌ ์ผ์ปซ๋ ๋ง

![Routing](https://www.sangoma.com/wp-content/uploads/how-ip-routing-works-diagram-1.png)

## ๐ PAGE ROUTING

![Standard](https://mobidev.biz/wp-content/uploads/2021/07/3-tier-web-architecture.jpg)

๊ธฐ๋ณธ์ ์ผ๋ก ํด๋ผ์ด์ธํธ๋ ์ด๋ค ์ฌ์ดํธ์ ๋ค์ด๊ฐ๊ฒ ๋๋ฉด ๊ทธ ์ฌ์ดํธ์ ์น์๋ฒ๋ก htmlํ์ผ์ ์์ฒญ์ ํ๊ฒ ๋๊ณ , ๊ทธ ์์ฒญ์ ๋ฐ์ ์น์๋ฒ๋ ์์ฒญ๋ฐ์ ํด๋ผ์ด์ธํธ๋ก ํ์ผ๋ค์ ๋ฟ๋ ค์ฃผ๊ฒ ๋๋ค.

### MPA (Multipage Application)

![MPA](https://mobidev.biz/wp-content/uploads/2021/07/ssr-web-app-architecture-diagram-1.jpg)

๋ฉํฐํ์ด์ง ์ดํ๋ฆฌ์ผ์ด์์ด๋ ์น์๋ฒ๊ฐ ๊ฐ๊ธฐ ๋ค๋ฅธ page๋ค์ html ํ์ผ๋ค์ ๊ฐ์ง๊ณ  ์๋ค๊ฐ ํด๋ผ์ด์ธํธ๊ฐ ํด๋น ํ์ด์ง์ GET ์์ฒญ์ ํ๋ฉด ๊ทธ๊ฒ์ ์ธ์ํ๊ณ  html ํ์ผ์ ๋ฟ๋ ค์ฃผ๋ ์ญํ ์ ํ๋๋ฐ ๋ธ๋ผ์ฐ์ ๋ ์๋ต์ ๋ฐ์ผ๋ฉด <mark>ํ๋ฉด์ด ๊น๋นก๊ฑฐ๋ฆผ๊ณผ ๋์์ ์ด๋ฅผ ๋๋๋ง ํ์ฌ ๋ณด์ฌ์ฃผ๊ฒ ๋๋ค</mark>

### SPA (Singlepage Application)

![SPA](https://mobidev.biz/wp-content/uploads/2021/07/spa-web-app-architecture-diagram.jpg)

๋ฉํฐํ์ด์ง ์ดํ๋ฆฌ์ผ์ด์๊ณผ๋ ๋ฐ๋๋ก ์น์๋ฒ๊ฐ ๋ง ๊ทธ๋๋ก ๋จ ํ๊ฐ์ง์ ํ์ด์ง๋ง ๊ฐ์ง๊ณ  ์์ฒญ์ ๋ฐ๋ผ index.html๋ง ๋ฟ๋ ค์ฃผ๋ ์ญํ ์ ํ๊ฒ๋๋ค. ๋ง์ฝ์ ํด๋ผ์ด์ธํธ๊ฐ ํ์ด์ง๋ฅผ ์ด๋ํ๊ณ  ์ถ๋ค๊ณ  ํด๋ ํ์ด์ง๊ฐ ํ๋๋ฐ์ ์๊ธฐ ๋๋ฌธ์ ์ง์ํด์ index.html๋ง ๋ฟ๋ ค์ฃผ๊ฒ ๋๋ค.

์๋ฅผ ๋ค์ด ํน์๋ ๋ด๊ฐ ์ด๋ค ์ฌ์ดํธ์์ ํ์ด์ง ์ด๋์ ํ๋ ค๊ณ  ๋ฒํผ์ ๋๋ ๋ค๊ณ  ์น์. ๊ทธ๋ผ ํด๋ผ์ด์ธํธ๋ ์๋์ผ๋ก GET ํน์ POST๋ก ํด๋น ๋ฆฌ์์ค๋ฅผ ์์ฒญํ๊ฒ ๋๋ค. ๊ทผ๋ฐ ์๋ ๊ฐ์์ผ๋ฉด ์น ์๋ฒ๊ฐ ์ด HTTP ๋ฉ์๋ ์์ฒญ์ ๋ฐ์์ ๋ฐ์ดํฐ๋ฒ ์ด์ค์ ์๋ ํด๋น ์์ฒญ html์ ์ฐพ์์ ๊ฐ์ ธ๋ค ์ฃผ๋ ๊ฒ์ด์ง๋ง SPA ๋ฐฉ์์ ํด๋ผ์ด์ธํธ ์์ฒญ์ด ๋ฐ๋ก REACT APP์ด ์๋์ผ๋ก ์์์ ํ์ด์ง๋ฅผ ์๋ฐ์ดํธ ์์ผ๋ฒ๋ฆฐ๋ค (์ปดํฌ๋ํธ๋ฅผ ๊ต์ฒด).

์ด๋ฐ ๋ฐฉ์์ผ๋ก ํ์ด์ง๋ฅผ ์ด๋ํ๊ฒ ๋๋ฉด ํ์ด์ง๋ฅผ ์ด๋ํ ๋๋ง๋ค ์น์๋ฒ๋ฅผ ํตํด ๊ธฐ๋ค๋ฆฌ๋ ์๊ฐ ์์ฒด๊ฐ ์ฌ๋ผ์ ธ๋ฒ๋ฆฌ๊ธฐ ๋๋ฌธ์ ์ฌ์ฉ์ ์์ฅ์์๋ ๋๋ฅด๋ ์ฆ์ ํ์ด์ง๊ฐ ๋ฐ๋๋ ๊ฒ์ ๊ฒฝํํ๊ฒ ๋๊ณ , ์ด๊ฑด ๋ง์น ํด๋ํฐ์์ ์ฑ์ ๋ฐ์์๋๋ฅผ ๋๊ฐ์ด ๊ฒฝํํ  ์ ์๊ฒ ๋๋ค. ํน์๋ ๊ฐ๊ฐ ํ์ด์ง์ ์ค์๊ฐ์ผ๋ก ๋ฐ์์ค๋ ๋ฐ์ดํฐ๊ฐ ํ์ํ  ๊ฒฝ์ฐ์๋ ์น์๋ฒ์ ๋ฐ์ดํฐ๋ง ์์ฒญํ๊ณ  ์ ๋ฌ ๋ฐ๊ฒ ๋๋ค. ํน์๋ ์๊ฐ์ด ๊ฑธ๋ฆฌ๋ ๊ท๋ชจ์ ๋ฐ์ดํฐ๋ผ๊ณ  ํด๋ ๋ก๋ฉํ์ด์ง๋ฅผ ๋์๋๊ณ  ๋ทฐ๋ผ๋ ๋จผ์  ๋ณด์ด๊ฒ๋ ํ๋ ๋ฐฉ๋ฒ๋ ์๋ค.

์ด๋ฐ ๋ฐฉ์์ ํด๋ผ์ด์ธํธ ์ธก์์ ์์์ ๋๋๋ง์ ํ๋ค๊ณ  ํด์ <mark>CSR (Client Side Rendering)</mark>์ด๋ผ๊ณ  ๋ถ๋ฅธ๋ค.

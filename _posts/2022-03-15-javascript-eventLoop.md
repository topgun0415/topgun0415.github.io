---
layout: post
title: Javascript Event Loop Mechanism
date: 2022-03-21 13:00 +0800
# last_modified_at: 2022-02-16 01:08:25 +0800
tags: [javascript]
toc: true
math: false
---

![Javascript](https://upload.wikimedia.org/wikipedia/commons/thumb/9/99/Unofficial_JavaScript_logo_2.svg/480px-Unofficial_JavaScript_logo_2.svg.png)

## 이벤트 루프(Event loop)란 무엇인가?

이벤틀 루프란 이것이다!

이벤트 루프 velog 참고 사이트 : https://velog.io/@titu/JavaScript-Task-Queue%EB%A7%90%EA%B3%A0-%EB%8B%A4%EB%A5%B8-%ED%81%90%EA%B0%80-%EB%8D%94-%EC%9E%88%EB%8B%A4%EA%B3%A0-MicroTask-Queue-Animation-Frames-Render-Queue

이벤트 루프 참고 해외 사이트 : http://latentflip.com/loupe/?code=ZnVuY3Rpb24gYWFhKCkgewogIHNldFRpbWVvdXQoKCkgPT4gewogICAgY29uc29sZS5sb2coJ2QnKTsKICB9LCAwKTsKICBjb25zb2xlLmxvZygnYycpOwp9CgpzZXRUaW1lb3V0KCgpID0%2BIHsKICBjb25zb2xlLmxvZygnYScpOwogIGFhYSgpOwp9LCAwKTsKCnNldFRpbWVvdXQoKCkgPT4gewogIGFhYSgpOwogIGNvbnNvbGUubG9nKCdiJyk7Cn0sIDApOwo%3D!!!PGJ1dHRvbj5DbGljayBtZSE8L2J1dHRvbj4%3D

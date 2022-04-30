---
emoji: 🪤
title: CSS_Flexbox
date: '2022-04-18 21:00:00'
author: bontaedev
tags: java web css study
categories: Web
---

## bootstrap

  <!-- 부트스트랩 요소를 가져다 사용할 때는
      1. css link, 혹은 script를 가져온다
      2. 클래스명을 지켜서 넣어야 한다. 함부로 바꾸지 않는다.
    -->

- ordering : breakpoint에 따라서 레이아웃 배치를 바꿔줄 때
  요소들에 order를 주고 그 순서에 맞게 배치하는 것이 가능
- 만약 화면의 크기가 바뀌었을 때
  보여주고 싶지 않은 요소 & 보여주고 싶은 요소를 결정하고 싶다면
  d 속성값을 사용한다. (display)

  d-none : col을 안보이게 하고 싶을 때
  d-md-block : md사이즈 이상일 때 태그에 block 속성을 가지게 한다.

  /_
  상대적 단위
  em : 본인 요소의 폰트 사이즈를 1em 가짐, 본인 요소가 글꼴 크기가 없으면
  부모요소를 기준으로 사이즈를 잡음
  rem : 루트요소(HTML)의 폰트사이즈를 기준으로 계산한 것이 1rem 계산
  _/

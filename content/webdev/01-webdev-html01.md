---
emoji: 🪤
title: HTML_태그 정리
date: '2022-04-15 20:23:45'
author: bontaedev
tags: java web study
categories: Web
---

> ## 국비과정 교육 중에서 HTML 파트를 공부하고 정리한 내용

## 웹페이지, 웹서비스

- 웹페이지 : 하나의 페이지. 웹페이지가 여러가지가 모여서 만들어지는 모음을 웹사이트라고 한다.

## HTML이란?

- HTML (Hyper Text Markup Language) : 웹페이지를 구성하는 언어
- Markup Language : 구조화된 언어 - 각각의 요소들을 태그로 구조화시킨 언어 A라는 태그를 보면 이런 의미를 가지고 있구나고 해석할 수 있다.

## HTTP

- HTTP (HyperText Transfer
  Protocol) : 웹에서 이뤄지는 모든 데이터교환(클라이언트-서버)은 통신규약을 통해 이루어짐.

## HTML 태그

```html
<input type="text" value="abc123" readonly />
```

- <a> : 하이퍼링크 요소 구성

  - target 속성으로 새로운 탭으로 이동할지, 새로운 브라우저를 열어 이동할지, 현재 창에서 이동할 지 속성 부여 가능 self, blanl
  - blank : 새로운 탭에서 열기

- <input> : 사용자의 입력값을 받기위해 사용하는 요소

  - placeholder : 어떤 값을 입력할 지 안내해주는 역할
  - value : 창에 실제로 입력되는 데이터
  - <radio>사용자의 입력값을 선택으로 받는 것, 여러개의 값 중 하나만 체크하게끔 하고싶을 때 사용. 똑같은 name 값을 부여하면 하나만 체크 가능
  - checked : 기본으로 이 항목을 선택해둠.
  - 여러개의 선택지에서 여러개의 선택값을 받고 싶다면 checkbox

- select : 여러개의 옵션값을 미리 깔아두고 사용자가 선택하게끔 하는 입력방식

```html
<input type="text" placeholder="id 입력" />
<input type="text" value="abc123" />
<input type="text" value="abc123" readonly />
<input type="text" maxlength="4" />

<p>input password</p>
<input type="password" />
<p>input email</p>
<input type="email" />

<!-- 사용자의 입력값을 선택으로 받는 것, 여러개의 값 중 하나만 체크하게끔 하고싶을 때 사용 
        똑같은 name 값을 부여하면 하나만 체크 가능
        checked : 기본으로 이 항목을 선택해둠.
    -->
<p>input radio</p>
<input type="radio" name="hobby" checked />등산 <input type="radio" name="hobby" />수영
<input type="radio" name="hobby" />서핑

<!-- 여러개의 선택지에서 여러개의 선택값을 받고 싶다면 checkbox -->
<p>input checkbox</p>
<input type="checkbox" name="dinner" />족발 <input type="checkbox" name="dinner" />치킨
<input type="checkbox" name="dinner" />국밥

<!-- select : 여러개의 옵션값을 미리 깔아두고 사용자가 선택하게끔 하는 입력방식 -->
<p>phone</p>
<select name="phone">
  <option value="010">010</option>
  <option value="011">011</option>
  <option value="017">017</option>
  <option value="017">018</option>
</select>
- <input type="text" maxlength="4" /> - <input type="text" maxlength="4" />

<p>Date</p>
<input type="date" />

<p>color</p>
<input type="color" />

<p>range</p>
<input type="range" />

<p>button</p>
<input type="button" value="버튼" />
<button>button2</button>
```

- 일반적으로 한 줄짜리 입력을 받을 때 사용
- textarea : 여러줄의 텍스트 입력값을 받을 때 사용

```html
<textarea style="width: 300px; height: auto; resize: none" placeholder="내용입력"></textarea>
```

<img src="" />
별도의 width, height 를 지정해주지 않으면 원본크기만큼 자리차지

문자 관련 태그

```html
<h1>제목1</h1>
<h6>제목6</h6>

<em>em</em>
<strong>strong</strong>
<mark>mark</mark>
<b>bold</b>
<i>italic</i>
<u>underline</u>
```

## HTML List

- List 목록
  - ul : unordered list 순서가 없는 리스트
  - ol : orderded list 순서가 있는 리스트
    type : 숫자, 아라비아 숫자, 알파벳 순서를 매길지 결정해줄 수 있음
    <start : 시작점 지정 가능>

## HTML Table

- table : 페이지의 레이아웃 잡는 용도. 현재는 게시판을 구성하는 용도로 쓰임

```html
<table>
  <!-- 한 행을 구성하기 위한 태그 -->
  <tr>
    <th>번호</th>
    <!-- 헤더 컬럼을 구성할 때-->
    <th>제목</th>
    <th>글쓴이</th>
    <th>날짜</th>
  </tr>
  <tr>
    <td>1</td>
    <!-- 테이블의 데이터를 구성할 때 -->
    <td>맑음</td>
    <td>당산맨</td>
    <td>2022-11-11</td>
  </tr>
  <tr>
    <td>2</td>
    <td>편백나무 스프레이</td>
    <td>건강웡</td>
    <td></td>
  </tr>
</table>
```

- html5 : Semantic tag를 적극 사용하도록 권장, 태그의 사용목적 자체를 명시해주는 태그

```html
<table border="1">
  <thead>
    <tr>
      <th>번호</th>
      <th>제목</th>
      <th>글쓴이</th>
      <th>날짜</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1</td>
      <td>맑음</td>
      <td>당산맨</td>
      <td>2022-11-11</td>
    </tr>
    <tr>
      <td>2</td>
      <td>편백나무 스프레이</td>
      <td>건강웡</td>
      <td></td>
    </tr>
  </tbody>
</table>
```

## HTML Form

```html
<form action="요청을 보낼 주소" method="get/post">
  <input type="text" name="id" />
</form>
```

- Form : 사용자에게 입력받아 그 테이터를 서버에 전송하고자 할 때 사용
- get/post : 데이터를 전송하는 방식
- form 태그 안쪽에 서버로 전송하고 싶은 용도의 태그들은 반드시 name이라는 속성를 가지고 있어야 함
- form을 서버에 제출하기 위해 submit을 해줘야 함

  1. submit 타입의 버튼을 사용
  2. submit() 함수를 사용하거나

## display 속성

- display 속성 : block , inline

  - block : 요소의 전후 줄바꿈을 한 후에 무조건 한 줄을 차지하는 속성
  - inline : 해당 태그가 가지고 있는 컨텐츠의 크기만큼 자리를 차지
    <!-- p, div, span -->
    <!-- margin : 바깥 여백 -->

    <!-- block 속성(16px 마진), div, span - inline 태그 -->

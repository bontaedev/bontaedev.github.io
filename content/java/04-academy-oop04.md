---
emoji: 🪤
title: 자바 객체지향 프로그래밍 정리 - 다형성, 상속
date: '2022-03-21 20:21:00'
author: bontaedev
tags: java webdev study
categories: java
---

> ## 자바 객체지향 프로그래밍과 관련된 부분을 학습하고 정리한 포스트입니다.

# 다형성

# 상속(inheritance)

- 기존의 클래스를 재활용해서 새로운 클래스를 작성하는 과정이다. 코드의 중복을 제거하고 코드의 재사용성을 높일 수 있다.

## 클래스 간의 포함관계

- 클래스 들 간에 상속하지 않고 재사용하는 방법도 있다.
- 클래스 들 간에 포함관계(Composition)를 맺어준다.
- 포함관계를 맺어주는 것은 한 클래스의 멤버변수로 다른 클래스의 참조변수를 선언하는 것을 뜻한다.

상속 vs 포함

- 상속관계 : ~은 ~이다 (is~a)
- 포함관계 : ~은 ~을 가지고 있다. (has~a)

```java
class Circle {
  int x;
  int y;
  int r;
}
// 위의 클래스를 아래와 같이 변형

class Point {
  int x;
  int y;
}
 class Circle {
   Point c = new Point(); // 포함관계
   int r;
 }
```

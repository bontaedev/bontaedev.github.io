---
emoji: 🪤
title: 자바 객체지향 프로그래밍 정리 01
date: '2022-03-11 22:21:00'
author: bontaedev
tags: java webdev study
categories: java
---

> ## 자바 객체지향 프로그래밍과 관련된 부분을 학습하고 정리한 포스트입니다.

# 객체지향 언어의 특징

- 코드의 재사용성이 높다 - 기존의 코드를 재활용 (상속)
- 코드의 관리가 용이하다 - 포함관계, 오버라이딩
- 신뢰성 높은 프로그래밍이 가능하다. - 제어자, 메서드 활용하여 코드의 중복을 제거

# 객체의 구성요소

- 속성(property) : 멤버변수, 특성, 필드, 상태
- 기능(function) : 메서드, 함수, 행위

# 클래스와 인스턴스

- 클래스 : 객체를 정의 해놓은 설계도. 객체를 생성하기 위해 사용된다.
- 클래스를 만든다 -> 자료형을 만든다.
- 인스턴스(객체) : 어떤 클래스로부터 만들어진 객체를 인스턴스라고 한다.
- 인스턴스 : new 연산자를 통해 heap영역 안에 저장할 수 있는 공간.
- laptop.brand = "LG"; // .을 찍어서 주소값으로 따라가 heap영역으로 간다.

# 추상화와 캡슐화

- 추상화 :

# 캡슐화를 구현하는 방법

> 사용자가 접근하면 안되는 데이터들을 내부적으로 숨기거나 접근을 제한.

1. 접근제한자 사용.
2. getter/setter 사용

# 접근제한자(Access Modifier)

- public : 외부, 모든 곳에서 접근 가능
- private : 반드시 해당 클래스 내부에서만 접근이 가능 (일반적)
- protected : 같은 패키지 혹은 자식 패키지 에서만 접근가능
- default : 같은 패키지 안에서는 접근 가능

# getter / setter

- 값을 얻어오거나 셋팅할 수 있는 함수
- 읽기 전용, 쓰기 전용
- getter/setter는 반드시 public으로 선언
- 이를 통해 들어오는 데이터와 나가는 데이터에 전처리 후처리를 해줄 수 있다.

# 생성자

- 리턴타입 없음
- 클래스명과 이름이 같음
- 인스턴스가 만들어질 때 생성자가 필드 공간들을 초기화 (기본값을 셋팅)
- 자바에서는 기본생성자를 명시하지 않아도 JVM이 추가해준다
- 대신 생성자를 오버로딩 해서 사용할 때는 기본 생성자를 따로 명시해줘야 한다. JVM이 따로 추가하지 않기 때문

```java
public Car() {}

public Car(String brand, int speed, int oil) {
	this.brand = brand;
	this.speed = speed;
	this.oil = oil;
}
```

# this.

-

```java
public void setBrand(String brand) {
		this.brand = brand;
		// 인스턴스안의 brand와 매개변수로 전해진 brand
		// this는 주소값. 즉 자기자신이라고 생각하자.
}
```

# 클래스변수

- 클래스 변수, 프로그램의 시작과 동시에 메모리에 올라간다.
- 남발하면 메모리 영역 관리가 어려워질 수 있다. 신중하게 사용

```java
public class Access01 {
	public String id;
	protected int age;
	private String nickname;
	String written_date;
	public static int view_count;

}
```

---
emoji: 🪤
title: 국비학원 9일차 회고
date: '2022-03-08 22:21:00'
author: bontaedev
tags: java webdev study
categories: 회고
---

> # 국비수업 9일차.

> ## 오늘은 함수 파트!

## 함수란? (Function)

- 자바에서 기능을 이야기하는 것
- 특정한 작업을 수행하기 위해서 모아놓은 명령문의 집합

함수의 구성

- 정의부 : 메서드에 대해 어떤 기능을 수행할지 설명해놓은 부분
  - 매개변수 : 호출부룰 통해 전달된 인자값을 받아주는 변수
  - 리턴 자료형 : 메서드명 왼쪽에 반환하고자 하는 자료형을 적는다.
  - return : 함수에서 수행한 결과를 돌려준다. return을 만나는 순간 결과값과 함께 메서드 영역을 벗어나 버림
- 호출부 : 정의된 메서드를 불러와서 사용하는 부분

<br>

함수를 사용하면 좋은 점

- 코드가 분리되므로 가독성이 좋아진다
- 유지보수하기에 좋다
- 코드의 재활용성이 높아진다.

```java
public static int plus(int i, int j) { // 정의부
		// 매개변수와 인자값의 자료형, 갯수는 반드시 일치해야 한다.
		// 리턴 자료형 : 메서드명 왼쪽에 반환하고자 하는 자료형을 적는다.

		return i+j;
		// return : 수행한 결과를 돌려준다.
		// return을 만나는 순간 결과값과 함께 메서드 영역을 벗어나 버림
	}
```

## 함수의 매개변수와 리턴값

```java
public static char getA() { // 매개변수가 없을 때
		return 'A';
}

public static void greeting() { // void 리턴값이 없을 때
		System.out.println("안녕하세요.");
}

public static void main(String[] args) {
		// 매개변수나 인자값이 있거나 없을 경우
    // 매개변수나 리턴값은 반드시 필수는 아니다.

		System.out.println(getA());
		greeting();
}

```

## 오버로딩(Overloading)

- 메서드가 정의됐을 때는 하나의 기능이 있음
- 기존의 메서드가 가지고 있는 기능에 추가적인 인자값이나 자료형의 변화를 줘서 기본적인 형태를 다양화할 수 있는 문법

```java
public static int plus(int num1, int num2) {
		return num1 + num2;
}
// 메서드 명은 같지만 매개변수의 개수가 다름 = 오버로딩
public static int plus(int num1, int num2, int num3) {
		return num1 + num2 + num3;
}
// 메서드 명은 같지만 매개변수의 자료형이 다름 = 오버로딩
public static int plus(double num1, double num2) {
	return (int)(num1 + num2);
}
// 메서드 명은 같지만 매개변수의 자료형과 개수가 다름 = 오버로딩
public static int plus(char char1, char char2, char char3) {
	return char1 + char2 + char3;
}
// 반환타입과 메서드명이 같기 때문에 매개변수가 없더라도 오버로딩 가능
public static int plus() {
	return 5 + 10;
}
```

<br>

- 오버로딩 성립이 안되는 경우 (반환타입이 다른 경우)

```java
// 리턴타입이 달라지고 매개변수의 형태도 달라지면 다른 메서드로써 같은 이름을 사용할 수 있다. (오버로딩 아님)
public static void plus(float num1, float num2) {
		float rs = num1 + num2;
}

public static void main(String[] args) {
	// 두 개의 정수를 더하는 메서드
	System.out.println( plus(10, 5) );
	// 세 개의 정수를 더하는 메서드
	System.out.println( plus(10, 5, 10) );
	// 두 개의 실수를 더하는 메서드
	System.out.println( plus(3.5, 1.5) );
	// 세 개의 char 데이터를 더하는 메서드
	System.out.println( plus('a', 'b', 'c') );
}
```

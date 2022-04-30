---
emoji: 🪤
title: 국비학원 4일차 회고
date: '2022-02-28 20:26:00'
author: bontaedev
tags: java webdev study
categories: 회고
---

> # 국비수업 4일차 때 배운 내용을 개인적으로 정리.

> ## String, 형변환, 연산자, Scanner 등의 내용을 다룰 예정

## String 데이터 타입

## 형변환(Casting)

- 형변환(Casting) : 데이터의 자료형을 변환하는 것
- 개발자가 데이터의 타입을 예측하지 못했을 때
- 개발자가 원하는 대로 데이터 타입을 사용하기 위해서 데이터타입을 변경

<br>

- 자동 형변환(promotion) : 작은 자료형에서 큰 자료형으로 변환이 이루어지는 경우
- 강제 형변환(down casting) : 큰 자료형에서 작은 자료형으로 변환이 이루어지는 경우 ( 데이터의 손실이 일어날 수 있음 )

```java
byte b1 = 127;
System.out.println("b1 : " + b1);
short s1 = b1; // 더 큰 자료형으로 대입 (casting)

// 강제 형변환 (down casting)
long l2 = 1234567890123L;
System.out.println(l2);
int i2 = (int)l2;
System.out.println(i2);
short s2 = (short)i2;
System.out.println(s2);
byte b2 = (byte)s2;
System.out.println(b2);
```

- 정수와 실수 사이 형변환

```java
// 정수 -> 실수로 형변환
int i3 = 50;
float f3 = i3;
System.out.println(f3);

// 실수 -> 정수로 형변환
double d4 = 3.14;
int i4 = (int)d4;
System.out.println(i4);
```

- char 자료형의 특징

```java
// char (ASCII code) : 실제로는 내부적으로 문자와 매칭되는 코드가 들어있음
char c5 = 'a';
System.out.println("c5 : " + c5);
int i5 = c5;
System.out.println("i5 : " + i5);
```

## 연산자

1. 산술연산자 (사칙연산 + - \* / %)
2. 대입연산자 (=, +=, -=, /=, \*=, %=)
3. 비교연산자 ( <, > <=, >=, ==, !=)
4. 증감연산자 (전위연산, 후위연산)
5. 논리연산자 (&& and || or)
6. 삼항연산자 (조건식A ? b : c)

<br>

- 산술연산

```java
System.out.println(a + b);
System.out.println(a - b);
System.out.println(a * b);
System.out.println(a / b); // 몫 연산
System.out.println(a % b); // 나머지 연산
```

- 비교연산

```java
int a = 10;
int b = 4;
int c = 4;

System.out.println("a > b " + (a > b));
System.out.println("a < b " + (a < b));
System.out.println("a == b " + (a == b));
System.out.println("a != b " + (a != b));
System.out.println("b <= c " + (b <= c ));

char c1 = 'a'; // 97
char c2 = 'A'; // 65
System.out.println(" c1 == c2 : " + (c1 == c2));
System.out.println(" c1 > c2 : " + (c1 > c2));

```

- String 값을 비교 (equals)
- String은 참조자료형이므로 대입연산자는 주소값끼리 비교함으로 비교가 불가능 따라서 equals 메서드로 비교한다.

```java
String str1 = "abc";
String str2 = "abc";
String str3 = "def";

System.out.println(str1.equals(str2));
System.out.println(str2.equals(str3));
```

## Scanner 객체

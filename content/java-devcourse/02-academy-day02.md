---
emoji: 😳
title: 국비학원 2~3일차 회고
date: '2022-02-25 18:26:00'
author: bontaedev
tags: java webdev study
categories: 회고
---

> # 국비수업 2~3일차 때 배운 내용을 개인적으로 정리.

> ## 자바 프로그래밍을 위한 환경 셋팅부터 변수파트 까지

## 1. 자바 환경설정 하는 법

- 자바 프로그래밍을 위해서 JDK가 필요함
- 기존에 Oracle JDK를 사용하고 있었지만, 최적의 환경셋팅을 위해 제거하고 OpenJDK 11을 설치하였음
- Windows환경에서는 [OpenJDK github repo](https://github.com/openjdk/jdk11u-dev) 에서 다운받아서 설치하고 환경변수 설정하면 됨
- 본인은 MacOS 환경에서 homebrew 사용해서 AdoptOpenJDK 다운받아서 설치
  <br><br>
- homebrew를 이용해 JDK 다운로드 방법

```shell
brew tap AdoptOpenJDK/openjdk
brew cask install <version>
```

- 이후 설치 완료되면 `java -version` 커맨드로 설치 잘 됐는지 확인
- JDK 설치가 완료되면 Eclipse 설치, 추후에 웹프로젝트를 위해 Java EE 버전을 사용

<br><br>

## 2. 자바로 hello world 출력하기

- File - New - Java Project 로 새 프로젝트 생성
- main 함수 안에 **println** 을 사용하여 문자를 출력할 수 있다.
- **print** : 같은 줄에 출력 / **println** : 다른 줄에 출력

```java
public static void main(String[] args) {
		System.out.println("hello world");
	}
```

<br><br>

## 3. 자바에서 문자(' ')와 문자열(" ")

```java
println('a'); // character
println("abc"); // String
println(""); // empty String
println(''); // error!
```

- 자바에서는 문자와 문자열을 표현하는 방법이 다르다.
- ''(single quotation)은 문자
- ""(double quotation)은 문자열
- 빈 문자열은 가능하지만 빈 문자는 불가능.

<br><br>

## 4. 문자열과 다른 데이터를 조합할 때 주의할 점

    "hello" + 15 + 10 // "hello1510"
    15 + 10 + "bye" // "25bye"

<br>

> ### 문자열을 + 연산자를 통해서 숫자와 같은 데이터와 조합할 경우 컴파일러에서는 **"왼쪽에서 오른쪽"** 으로 계산된다. 데이터가 조합될 때 형변환이 이루어지기 때문인 듯.

<br><br>

## 5. 변수(Variable)

> ## 메모리에 데이터 값을 기록하는 공간

`int a = 10;`

- 변수의 선언 : 메모리에 데이터를 저장할 공간을 할당하는 것.
- 값 대입 : 생성한 메모리공간 (변수공간) 에 데이터를 넣는 것. 대입연산자(=)를 사용한다.
- 변수의 초기화 : 변수를 선언하고 처음으로 값을 대입하면 초기화가 이루어진다.

> ### 👉 일반적으로는 **변수선언과 동시에 기본값**으로 초기화 하는 것을 권장한다.

<br>

## 6. 데이터 타입(Data Type)

![javadata](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20191105122725/Primitive-Data-Types-in-Java-4.jpg)<center> _<자바 데이터 타입>_</center>

- 변수를 통해 저장공간을 할당할 때 저장할 크기에 대한 기준이 있어야 한다.
- 데이터에 대한 기준이 있어야 처리하기 쉽다.
- 아래는 기본 데이터 타입(Primitive Type)이다.

<br>

```java
// boolean
boolean t = true;
boolean f = false;

// character type
char c1 = 'a';
char c2 = '가';
char c3 = '5';

// 정수, 실수형 타입
byte b1 = -128;
byte b2 = 127;
short s1 = -32768;
short s2 = 32767;

System.out.println(100) // int는 정수 대표타입

long l1 = 321321321;
long l2 = 321321321321321L;

double d1 = 3.14; // double은 실수 대표타입
float f1 = 3.14f;
```

<br>

## 추가 1. 변수명 지을 때 알아둘 점

> ## 변수명을 지을 때 지켜야 할 규칙이 있다

- 첫글자는 숫자로 시작 x
- 특수문자로 시작 x
- 길이 제한은 없지만 짧고 의미있게 지을 것!

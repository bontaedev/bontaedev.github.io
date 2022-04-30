---
emoji: 🪤
title: 자바 예외처리
date: '2022-03-22 21:11:00'
author: bontaedev
tags: java webdev study
categories: java
---

> ## 자바 예외처리ㅋ

# 8.1 프로그램 에러 종류

- 컴파일 에러: 컴파일 중에 발생하는 에러
- 런타임 에러: 프로그램 실행 도중에 발생하는 에러
- 논리적 에러: 실행은 잘되나 의도한 것과 다르게 작동할 때

```java
System.out.println(args[0]);
```

자바의 런타임 에러

- error : 프로그램 코드에 의해 수습될 수 없는 심각한 오류
- exception : 코드에 의해 수습될 수 있는 미약한 오류

에러는 발생하면 프로그램의 비정상적 종료를 막을 수 없지만 예외는 예외처리를 통해 종료를 막을 수 잇다.

에러 ex. OutOfMemoryError, StackOverflowError

+) 컴파일러가 하는 일

- 구문체크, 번역, 최적화, 생략된 코드들을 추가

## Exception 클래스의 계층구조

- Exception
- IOException, ClassNotFoundException
- RuntimeException
  - ArithmeticException
  - ClassCastException
  - NullPointerException
  - IndexOutOfBoundsException

# Exception과 RuntimeException

- RuntimeException : 프로그래머의 실수에 의해 발생할 수 있는 예외
  ex. IndexOutOfBoundsException, NullPointException, ClassCastException, ArithmeticException
- Exception클래스 : 사용자와 같은 외부의 영향으로 발생할 수 있는 예외
  ex. FileNotFoundException, ClassNotFoundException, DataFormatException

# 예외처리 : try-catch

- 예외처리: 프로그램 실행시 발생할 수 있는 예외의 발생한 대비한 코드를 작성하는 것
- 비정상적인 종료를 막고 실행상태를 유지하기 위해
- 처리하지 못한 예외는 JVM의 예외처리기(UncaughtExceptionHandler)가 받아서 원인을 화면에 출력

## 예외처리 과정

- 첫번째 catch블록부터 차례로 내려가면서 catch블록 내의 괄호에 선언된 참조변수의 종류와 생성된 예외클래스의 인스턴스에 instanceof 연산자를 통해 검사
- 검사결과 true인 catch블록을 만날 때까지 검사하고, 찾으면 블럭의 문장을 모두 수행한 후에 try-catch문을 빠져나가고 예외는 처리

# finally

- Try-catch문과 함께 예외 발생여부와 상관없이 실행해야 할 코드를 포함시킬 목적으로 만들어짐

```java
Ex.

try {
  //   예외가 발생할 가능성이 있는 코드
} catch (Exception e) { // 인스턴스 e에 instanceof연산자를 통해 검사
  // 예외처리를 위한 코드
} finally {
  // 예외와 상관없이 실행되는 코드
  // finally문은 try-catch의 마지막 문단에 위치
}
```

# printStackTrace(), getMessage()

- 예외 발생시 예외 객체가 생성되고 메서드를 통해 확인할 수 있다.
- printStackTrace() : 예외발생 당시의 호출스택 call stack에 있었던 메서드의 정보와 예외 메세지를 화면에 출력
- getMessage() : 발생한 예외 클래스의 인스턴스에 저장된 메세지를 얻을 수 있다.

## 멀티 catch 블록 (JDK1.7)

```java
try {
} catch (ExceptionA | ExceptionB e) {
e.printStackTrace();
}
```

## throw 예외 발생시키기

- new를 통해서 예외 클래스 객체를 만든다음
- throw를 통해서 예외를 발생시킨다

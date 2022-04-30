---
emoji: 🪤
title: 자바 열거형(Enums)
date: '2022-03-21 21:11:00'
author: bontaedev
tags: java webdev study
categories: java
---

## 열거형(Enums)

```java
enum 열거형이름 {상수명1, 상수명2, ...}

enum Direction {EAST, SOUTH, WEST, ...}
```

- 자바에서는 타입에 안전한 열거형 (typesafe enum)
- 열거형에서는 상수간의 비교여서 ==를 사용할 수 있다.
- 비교연산자 <,> 는 사용할 수 없지만 compareTo()를 사용
- compareTo() : 왼쪽이 크면 양수, 오른쪽이 크면 음수

## 열거형의 조상 - java.lang.Enum

```java
Direction[] dArr = Direction.values()
for(Direction d : dArr)
  System.out.printf("%s=%d%n", d.name(), d.ordinal());
```

```java
Direction[] d = Direction.valueOf("WEST");
System.out.println(Direction.WEST==Direction.valueOf("WEST")); // true
```

- values() : 열거형의 모든 상수를 배열에 담아 반환
- getDeclaringClass() : 열거형의 Class 객체를 반환
- name() : 열거형 상수의 이름을 문자열로 반환
- ordinal() : 열거형 상수가 정의된 순서를 반환
- valueOf(Class<T> enumType, String name) : 지정한 열거형에서 name과 일치하는 열거형 상수를 반환

## 열거형에 멤버 추가

```java
enum Direction {
  EAST(1), SOUTH(5), WEST(-1), NORTH(10); // 끝에 ;을 추가

  private final int value; // 인스턴스 변수
  Direction(int value) { this.value = value; } // 생성자

  public int getValue() {return value;}
}

Direction d = new Direction(1);
// error (열거형의 생성자는 외부에서 호출할 수 없다. 묵시적으로 private 생성자이기 때문)
```

- 열거형 상수를 정의할 때 값이 불규칙하면, 원하는 값을 괄호로 상수 이름 옆에 붙여준다. ordinal 대신 이 값을 사용.
- 열거형 상수를 모두 정의한 후에 인스턴스 변수와 생성자를 정의
- 열거형의 멤버는 상수가 될 것이므로 인스턴스 변수를 final로 지정

## 추상메서드를 추가한 열거형

```java
enum Transportation {
  BUS(100) { int fare(int distance) {return distance*BASIC_FARE;} };
  TRAIN(150) { int fare(int distance) {return distance*BASIC_FARE;} };
  SHIP(100) { int fare(int distance) {return distance*BASIC_FARE;} };
  AIRPLAIN(300) { int fare(int distance) {return distance*BASIC_FARE;} };

  abstract int fare(int distance); // 거리에 따른 요금을 계산하는 추상메서드

  protected final int BASIC_FARE; // protected로 변경해 각 상수가 접근할 수 있도록

  Transportation(int basicFare) {
    BASIC_FARE = basicFare;
  }

  public int getBasicFare() { return BASIC_FARE; }
}

class EnumExam3 {
  public static void main(String[] args) {
    System.out.println("bus fare=")
  }
}
```

## 열거형의 이해

- 열거형 상수 하나하나가 객체로 취급한다.
- 즉 각 상수의 값은 객체의 주소를 가리키고 변하지 않기 때문에 == 로 비교가 가능

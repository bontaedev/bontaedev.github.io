---
emoji: πͺ€
title: μλ° μ΄κ±°ν(Enums)
date: '2022-03-21 21:11:00'
author: bontaedev
tags: java webdev study
categories: java
---

## μ΄κ±°ν(Enums)

```java
enum μ΄κ±°νμ΄λ¦ {μμλͺ1, μμλͺ2, ...}

enum Direction {EAST, SOUTH, WEST, ...}
```

- μλ°μμλ νμμ μμ ν μ΄κ±°ν (typesafe enum)
- μ΄κ±°νμμλ μμκ°μ λΉκ΅μ¬μ ==λ₯Ό μ¬μ©ν  μ μλ€.
- λΉκ΅μ°μ°μ <,> λ μ¬μ©ν  μ μμ§λ§ compareTo()λ₯Ό μ¬μ©
- compareTo() : μΌμͺ½μ΄ ν¬λ©΄ μμ, μ€λ₯Έμͺ½μ΄ ν¬λ©΄ μμ

## μ΄κ±°νμ μ‘°μ - java.lang.Enum

```java
Direction[] dArr = Direction.values()
for(Direction d : dArr)
  System.out.printf("%s=%d%n", d.name(), d.ordinal());
```

```java
Direction[] d = Direction.valueOf("WEST");
System.out.println(Direction.WEST==Direction.valueOf("WEST")); // true
```

- values() : μ΄κ±°νμ λͺ¨λ  μμλ₯Ό λ°°μ΄μ λ΄μ λ°ν
- getDeclaringClass() : μ΄κ±°νμ Class κ°μ²΄λ₯Ό λ°ν
- name() : μ΄κ±°ν μμμ μ΄λ¦μ λ¬Έμμ΄λ‘ λ°ν
- ordinal() : μ΄κ±°ν μμκ° μ μλ μμλ₯Ό λ°ν
- valueOf(Class<T> enumType, String name) : μ§μ ν μ΄κ±°νμμ nameκ³Ό μΌμΉνλ μ΄κ±°ν μμλ₯Ό λ°ν

## μ΄κ±°νμ λ©€λ² μΆκ°

```java
enum Direction {
  EAST(1), SOUTH(5), WEST(-1), NORTH(10); // λμ ;μ μΆκ°

  private final int value; // μΈμ€ν΄μ€ λ³μ
  Direction(int value) { this.value = value; } // μμ±μ

  public int getValue() {return value;}
}

Direction d = new Direction(1);
// error (μ΄κ±°νμ μμ±μλ μΈλΆμμ νΈμΆν  μ μλ€. λ¬΅μμ μΌλ‘ private μμ±μμ΄κΈ° λλ¬Έ)
```

- μ΄κ±°ν μμλ₯Ό μ μν  λ κ°μ΄ λΆκ·μΉνλ©΄, μνλ κ°μ κ΄νΈλ‘ μμ μ΄λ¦ μμ λΆμ¬μ€λ€. ordinal λμ  μ΄ κ°μ μ¬μ©.
- μ΄κ±°ν μμλ₯Ό λͺ¨λ μ μν νμ μΈμ€ν΄μ€ λ³μμ μμ±μλ₯Ό μ μ
- μ΄κ±°νμ λ©€λ²λ μμκ° λ  κ²μ΄λ―λ‘ μΈμ€ν΄μ€ λ³μλ₯Ό finalλ‘ μ§μ 

## μΆμλ©μλλ₯Ό μΆκ°ν μ΄κ±°ν

```java
enum Transportation {
  BUS(100) { int fare(int distance) {return distance*BASIC_FARE;} };
  TRAIN(150) { int fare(int distance) {return distance*BASIC_FARE;} };
  SHIP(100) { int fare(int distance) {return distance*BASIC_FARE;} };
  AIRPLAIN(300) { int fare(int distance) {return distance*BASIC_FARE;} };

  abstract int fare(int distance); // κ±°λ¦¬μ λ°λ₯Έ μκΈμ κ³μ°νλ μΆμλ©μλ

  protected final int BASIC_FARE; // protectedλ‘ λ³κ²½ν΄ κ° μμκ° μ κ·Όν  μ μλλ‘

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

## μ΄κ±°νμ μ΄ν΄

- μ΄κ±°ν μμ νλνλκ° κ°μ²΄λ‘ μ·¨κΈνλ€.
- μ¦ κ° μμμ κ°μ κ°μ²΄μ μ£Όμλ₯Ό κ°λ¦¬ν€κ³  λ³νμ§ μκΈ° λλ¬Έμ == λ‘ λΉκ΅κ° κ°λ₯

---
emoji: πͺ€
title: κ΅­λΉνμ 4μΌμ°¨ νκ³ 
date: '2022-02-28 20:26:00'
author: bontaedev
tags: java webdev study
categories: νκ³ 
---

> # κ΅­λΉμμ 4μΌμ°¨ λ λ°°μ΄ λ΄μ©μ κ°μΈμ μΌλ‘ μ λ¦¬.

> ## String, νλ³ν, μ°μ°μ, Scanner λ±μ λ΄μ©μ λ€λ£° μμ 

## String λ°μ΄ν° νμ

## νλ³ν(Casting)

- νλ³ν(Casting) : λ°μ΄ν°μ μλ£νμ λ³ννλ κ²
- κ°λ°μκ° λ°μ΄ν°μ νμμ μμΈ‘νμ§ λͺ»νμ λ
- κ°λ°μκ° μνλ λλ‘ λ°μ΄ν° νμμ μ¬μ©νκΈ° μν΄μ λ°μ΄ν°νμμ λ³κ²½

<br>

- μλ νλ³ν(promotion) : μμ μλ£νμμ ν° μλ£νμΌλ‘ λ³νμ΄ μ΄λ£¨μ΄μ§λ κ²½μ°
- κ°μ  νλ³ν(down casting) : ν° μλ£νμμ μμ μλ£νμΌλ‘ λ³νμ΄ μ΄λ£¨μ΄μ§λ κ²½μ° ( λ°μ΄ν°μ μμ€μ΄ μΌμ΄λ  μ μμ )

```java
byte b1 = 127;
System.out.println("b1 : " + b1);
short s1 = b1; // λ ν° μλ£νμΌλ‘ λμ (casting)

// κ°μ  νλ³ν (down casting)
long l2 = 1234567890123L;
System.out.println(l2);
int i2 = (int)l2;
System.out.println(i2);
short s2 = (short)i2;
System.out.println(s2);
byte b2 = (byte)s2;
System.out.println(b2);
```

- μ μμ μ€μ μ¬μ΄ νλ³ν

```java
// μ μ -> μ€μλ‘ νλ³ν
int i3 = 50;
float f3 = i3;
System.out.println(f3);

// μ€μ -> μ μλ‘ νλ³ν
double d4 = 3.14;
int i4 = (int)d4;
System.out.println(i4);
```

- char μλ£νμ νΉμ§

```java
// char (ASCII code) : μ€μ λ‘λ λ΄λΆμ μΌλ‘ λ¬Έμμ λ§€μΉ­λλ μ½λκ° λ€μ΄μμ
char c5 = 'a';
System.out.println("c5 : " + c5);
int i5 = c5;
System.out.println("i5 : " + i5);
```

## μ°μ°μ

1. μ°μ μ°μ°μ (μ¬μΉμ°μ° + - \* / %)
2. λμμ°μ°μ (=, +=, -=, /=, \*=, %=)
3. λΉκ΅μ°μ°μ ( <, > <=, >=, ==, !=)
4. μ¦κ°μ°μ°μ (μ μμ°μ°, νμμ°μ°)
5. λΌλ¦¬μ°μ°μ (&& and || or)
6. μΌν­μ°μ°μ (μ‘°κ±΄μA ? b : c)

<br>

- μ°μ μ°μ°

```java
System.out.println(a + b);
System.out.println(a - b);
System.out.println(a * b);
System.out.println(a / b); // λͺ« μ°μ°
System.out.println(a % b); // λλ¨Έμ§ μ°μ°
```

- λΉκ΅μ°μ°

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

- String κ°μ λΉκ΅ (equals)
- Stringμ μ°Έμ‘°μλ£νμ΄λ―λ‘ λμμ°μ°μλ μ£Όμκ°λΌλ¦¬ λΉκ΅ν¨μΌλ‘ λΉκ΅κ° λΆκ°λ₯ λ°λΌμ equals λ©μλλ‘ λΉκ΅νλ€.

```java
String str1 = "abc";
String str2 = "abc";
String str3 = "def";

System.out.println(str1.equals(str2));
System.out.println(str2.equals(str3));
```

## Scanner κ°μ²΄

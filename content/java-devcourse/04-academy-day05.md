---
emoji: ๐ชค
title: ๊ตญ๋นํ์ 5์ผ์ฐจ ํ๊ณ 
date: '2022-03-02 14:26:00'
author: bontaedev
tags: java webdev study
categories: ํ๊ณ 
---

> # ๊ตญ๋น์์ 5์ผ์ฐจ ๋ ๋ฐฐ์ด ๋ด์ฉ์ ๊ฐ์ธ์ ์ผ๋ก ์ ๋ฆฌ.

> ## ์ค๋์ ์๋ฐ์ ์ ์ด๋ฌธ ์ค ๋ฐ๋ณต๋ฌธ์ ๋ํด ๋ฐฐ์ ์.

[1. for](#1-for)
[2. while](#2-while)

## 1. ๋ฐ๋ณต๋ฌธ(Loop)

`for(int i = 0; int < 10; i++)`

- ํ๋ก๊ทธ๋จ์ ํ๋ฆ์ ๋ฐ๋ณต์์ผ์ฃผ๋ ์ ์ด๋ฌธ.
- ๋ฐ๋ณต๋ฌธ์ ์กฐ๊ฑด์์ ์ถฉ์กฑํ๋ ๋์์ ์ค๊ดํธ ๋ด์ ์ฝ๋๊ฐ ๋ฐ๋ณต๋์ด ์คํํ๋ค.
- ์กฐ๊ฑด์์ ๋ถ์ถฉ์กฑํ๋ ์๊ฐ ๋ฐ๋ณต๋ฌธ์ ๋ฒ์ด๋ ์๋ ์ฝ๋ ํ๋ฆ์ผ๋ก ๋์๊ฐ๋ค.
- ์กฐ๊ฑด์์ ์ถฉ์กฑ์ํค๋ฉด ์์ชฝ ์ฝ๋๊ฐ ์คํ๋๊ณ  ๋๋๊ธฐ ์ง์ ์ ์ฆ๊ฐ์์ด ์คํ๋๋ ์์์ด๋ค.

### 1. for

```java
for(์ด๊ธฐ์; ์กฐ๊ฑด์; ์ฆ๊ฐ์){
  // ์คํ์ฝ๋
}
```

- ์ด๊ธฐ์ : ๋ช ๋ฒ๋ถํฐ ์์ํ ๊ฑด์ง
- ์กฐ๊ฑด์ : ์ธ์ ๊น์ง ๋ฐ๋ณตํ ๊ฑด์ง
- ์ฆ๊ฐ์ : ์์ชฝ ์ฝ๋๊ฐ ๋ฐ๋ณต๋  ๋๋ง๋ค ํ๋ฒ์ฉ ์คํ

<br>

### 2. while

```java
Scanner sc = new Scanner(System.in);
String input = "";

while (!input.equals("q")) {
			System.out.print("์๋ ฅํ์ธ์ > ");
			input = sc.nextLine();
			System.out.println("1");
		}
		System.out.println("์ข๋ฃ");
```

- ์กฐ๊ฑด์๋ง ์๊ตฌํ๋ ๋ฐ๋ณต๋ฌธ, ์ด๊ธฐ์๊ณผ ์ฆ๊ฐ๋ฌธ์ ์์ด๋ ๋๋ค.
- ์ธ์ ๊น์ง ์ฝ๋๋ฅผ ๋ฐ๋ณตํด์ผ ํ ์ง ๋ชจ๋ฅผ ๋, ํน๋ณํ ์ผ์ด ์ผ์ด๋์ง ์์ ๋๊น์ง ์ฝ๋ ๋ฐ๋ณต.
- ๋ณดํต ๋ฌดํ๋ฃจํ๋ฅผ ๊ตฌํํ๊ธฐ ์ํด ๋ง์ด ์ฌ์ฉ

## ์์  ๋ฌธ์ 

### ์์  1. 1๋ถํฐ ์ฌ์ฉ์๊ฐ ์๋ ฅํ ๊ฐ๊น์ง ๋ฐ๋ณต

```java
Scanner sc = new Scanner(System.in);
System.out.print("๊ฐ์ ์๋ ฅ > ");
int num = Integer.parseInt(sc.nextLine());

for (int i = 0; i < num+1; i++) {
	System.out.print(i + " ");
}
```

<br>

### ์์  2. 1๋ถํฐ ์ฌ์ฉ์๊ฐ ์๋ ฅํ ๊ฐ์์ 'ํ์'๋ง ์ถ๋ ฅ

```java
Scanner sc = new Scanner(System.in);

System.out.print("๊ฐ์ ์๋ ฅ > ");
int num2 = Integer.parseInt(sc.nextLine());

// ํ์์ผ ๋๋ง ์ถ๋ ฅ
for (int i = 1; i < num2+1; i++) {
	if (i%2 == 1) System.out.print(i + " ");
}
```

- ๋๋จธ์ง ์ฐ์ฐ์ผ๋ก '๋๋จธ์ง๊ฐ 1์ด ๋จ์ผ๋ฉด ํ์'์ด๋ฏ๋ก ์ด๋ฅผ ์ด์ฉํด์ ์ฐ์ฐ

<br>

### ์์  3. ์ฆ๊ฐ๋ฌธ์ 2์ฉ ์ฆ๊ฐ์ํฌ๋ ค๋ฉด

```java
for (int i = 1; i < num2+1; i+=2) {
			System.out.print(i + " ");
}
```

<br>

### ์์  4. 1๋ถํฐ 5๊น์ง ์ถ๋ ฅํ๋๋ฐ 3์ ์ ์ธ (continue)

<br>

### ์์  5. ์๋ ฅ๊ฐ์ ๋ฐ๊ณ  1๋ถํฐ ์ฌ์ฉ์ ์๋ ฅ๊ฐ๊น์ง ์ ์ฒดํฉ์ ์ถ๋ ฅ

```java
int inputNum = 0;
int sum = 0;

Scanner sc = new Scanner(System.in);
System.out.print("์๋ ฅ >  ");
inputNum = Integer.parseInt(sc.nextLine());

for (int i = 1; i <= inputNum; i++) {
	System.out.print(i + " ");
	sum += i;
}
System.out.println(sum);
```

- ์๋ ฅ๊ฐ๊ณผ ํฉ์ ๊ณ์ฐํ  ๋ณ์๋ฅผ ๋จผ์  ์ ์ธํ๋ค.
- sum์ ๋ณตํฉ์ฐ์ฐ์๋ฅผ ์ด์ฉํด ๋ฐ๋ณต๋ฌธ์ ๋๋ฆฌ๋ฉด์ 1๋ถํฐ ์ฐจ๋ก๋๋ก ๋ํด์ค๋ค. ๊ธฐ๋ณธ์ ์ธ ํฉ ์ฐ์ฐ ๊ตฌํ

### ์ค์ต1.

`gist:bontaedev/616d5e690d313e489dfef4040d5eb15a#day04_ex01.java`

```java
Scanner sc = new Scanner(System.in);

		int balance = 3000;
		int money = 0;
		int select = 0;

		while (true) {
			System.out.println("=== ATM ์๋ฎฌ๋ ์ดํฐ ===");
			System.out.println("1. ์์ก์กฐํ");
			System.out.println("2. ์๊ธํ๊ธฐ");
			System.out.println("3. ์ถ๊ธํ๊ธฐ");
			System.out.println("4. ์ข๋ฃํ๊ธฐ");

			System.out.print(">> ");
			select = Integer.parseInt(sc.nextLine());

			switch (select) {
				case 1:
					System.out.println("ํ์ฌ ๋ณด์ ์์ก์ " + balance + "์๋๋ค.\n");
					continue;
				case 2:
					System.out.print("์ผ๋ง๋ฅผ ์๊ธํ์๊ฒ ์ต๋๊น? > ");
					money = Integer.parseInt(sc.nextLine());
					balance += money;
					System.out.println(money + " ์์ด ์๊ธ๋์์ต๋๋ค.\n");
					continue;
				case 3:
					System.out.print("์ผ๋ง๋ฅผ ์ถ๊ธํ์๊ฒ ์ต๋๊น? > ");
					money = Integer.parseInt(sc.nextLine());
					balance -= money;
					System.out.println(money + " ์์ด ์ถ๊ธ๋์์ต๋๋ค.\n");
					continue;
				case 4:
					System.out.println("๊ฑฐ๋๊ฐ ์ข๋ฃ๋์์ต๋๋ค.");
					break;
				default:
					System.out.println("์ ํจํ ๋ฒํธ๊ฐ ์๋๋๋ค.\n");
			}
		}
```

```toc

```

---
emoji: 🪤
title: 국비학원 5일차 회고
date: '2022-03-02 14:26:00'
author: bontaedev
tags: java webdev study
categories: 회고
---

> # 국비수업 5일차 때 배운 내용을 개인적으로 정리.

> ## 오늘은 자바의 제어문 중 반복문에 대해 배웠음.

[1. for](#1-for)
[2. while](#2-while)

## 1. 반복문(Loop)

`for(int i = 0; int < 10; i++)`

- 프로그램의 흐름을 반복시켜주는 제어문.
- 반복문은 조건식을 충족하는 동안은 중괄호 내의 코드가 반복되어 실행한다.
- 조건식을 불충족하는 순간 반복문을 벗어나 원래 코드 흐름으로 돌아간다.
- 조건식을 충족시키면 안쪽 코드가 실행되고 끝나기 직전에 증감식이 실행되는 순서이다.

### 1. for

```java
for(초기식; 조건식; 증감식){
  // 실행코드
}
```

- 초기식 : 몇 번부터 시작할건지
- 조건식 : 언제까지 반복할건지
- 증감식 : 안쪽 코드가 반복될 때마다 한번씩 실행

<br>

### 2. while

```java
Scanner sc = new Scanner(System.in);
String input = "";

while (!input.equals("q")) {
			System.out.print("입력하세요 > ");
			input = sc.nextLine();
			System.out.println("1");
		}
		System.out.println("종료");
```

- 조건식만 요구하는 반복문, 초기식과 증감문은 없어도 된다.
- 언제까지 코드를 반복해야 할지 모를 때, 특별한 일이 일어나지 않을 때까지 코드 반복.
- 보통 무한루프를 구현하기 위해 많이 사용

## 예제 문제

### 예제 1. 1부터 사용자가 입력한 값까지 반복

```java
Scanner sc = new Scanner(System.in);
System.out.print("값을 입력 > ");
int num = Integer.parseInt(sc.nextLine());

for (int i = 0; i < num+1; i++) {
	System.out.print(i + " ");
}
```

<br>

### 예제 2. 1부터 사용자가 입력한 값에서 '홀수'만 출력

```java
Scanner sc = new Scanner(System.in);

System.out.print("값을 입력 > ");
int num2 = Integer.parseInt(sc.nextLine());

// 홀수일 때만 출력
for (int i = 1; i < num2+1; i++) {
	if (i%2 == 1) System.out.print(i + " ");
}
```

- 나머지 연산으로 '나머지가 1이 남으면 홀수'이므로 이를 이용해서 연산

<br>

### 예제 3. 증감문을 2씩 증가시킬려면

```java
for (int i = 1; i < num2+1; i+=2) {
			System.out.print(i + " ");
}
```

<br>

### 예제 4. 1부터 5까지 출력하는데 3은 제외 (continue)

<br>

### 예제 5. 입력값을 받고 1부터 사용자 입력값까지 전체합을 출력

```java
int inputNum = 0;
int sum = 0;

Scanner sc = new Scanner(System.in);
System.out.print("입력 >  ");
inputNum = Integer.parseInt(sc.nextLine());

for (int i = 1; i <= inputNum; i++) {
	System.out.print(i + " ");
	sum += i;
}
System.out.println(sum);
```

- 입력값과 합을 계산할 변수를 먼저 선언한다.
- sum에 복합연산자를 이용해 반복문을 돌리면서 1부터 차례대로 더해준다. 기본적인 합 연산 구현

### 실습1.

`gist:bontaedev/616d5e690d313e489dfef4040d5eb15a#day04_ex01.java`

```java
Scanner sc = new Scanner(System.in);

		int balance = 3000;
		int money = 0;
		int select = 0;

		while (true) {
			System.out.println("=== ATM 시뮬레이터 ===");
			System.out.println("1. 잔액조회");
			System.out.println("2. 입금하기");
			System.out.println("3. 출금하기");
			System.out.println("4. 종료하기");

			System.out.print(">> ");
			select = Integer.parseInt(sc.nextLine());

			switch (select) {
				case 1:
					System.out.println("현재 보유잔액은 " + balance + "입니다.\n");
					continue;
				case 2:
					System.out.print("얼마를 입금하시겠습니까? > ");
					money = Integer.parseInt(sc.nextLine());
					balance += money;
					System.out.println(money + " 원이 입금되었습니다.\n");
					continue;
				case 3:
					System.out.print("얼마를 출금하시겠습니까? > ");
					money = Integer.parseInt(sc.nextLine());
					balance -= money;
					System.out.println(money + " 원이 출금되었습니다.\n");
					continue;
				case 4:
					System.out.println("거래가 종료되었습니다.");
					break;
				default:
					System.out.println("유효한 번호가 아닙니다.\n");
			}
		}
```

```toc

```

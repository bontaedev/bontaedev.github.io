---
emoji: 🪤
title: 국비학원 8일차 회고
date: '2022-03-07 21:26:00'
author: bontaedev
tags: java webdev study
categories: 회고
---

> # 국비수업 8일차.

> ## 오늘은 새롭게 나가는 배열 파트!

## 배열(Array)이란?

같은 타입의 데이터를 연속된 공간에 나열시키고, 데이터 각각을 인덱스라는 걸 이용해서 사용할 수 있도록 만들어 놓은 자료구조이다. 변수는 한개의 원시 데이터만 저장할 수 있지만 배열에서 부터는 여러 개의 데이터를 한번에 저장해서 쓸 수 있다.

- 배열 선언하기 : 선언은 `DataType[] arrayname;` 같은 형태로 하면 된다.
- 배열 초기화 : new 연산자를 통해 heap 공간에 생성하고 참조변수에 주소값을 대입한다.

```java
int[] arr = new int[5];
```

<br>

위 내용을 설명하자면 대입연산자(=) 왼쪽은 int형 데이터들을 저장할 수 있는 배열의 '주소값'을 저장하는 변수를 만드는 것이다. 이걸 **참조변수** 라고 부르는데 여기는 배열을 찾아갈 주소가 담기는 공간 이라고 생각하면 된다.

그럼 배열은 어디있냐고? 대입연산자 오른쪽에 new 연산자를 통해 메모리의 heap영역이라는 곳에 배열이라는 자료구조 (위의 경우에는 5칸) 가 생성된다. 그리고 그 배열을 찾아갈 수 있는 주소를 arr 변수에다 저장하는 것이다. 위와 같이 배열을 생성할 때는 반드시 '얼마만큼 생성할 건지' 명시해줘야 한다.

<br>

```java
int[] arr2 = new int[] {1,2,3,4,5};
int[] arr3 = {1,2,3,4,5};
String[] arr5 = new String[] {"a","b","c"}
```

<br>

- 선언과 동시에 초기화하는 방법은 위와 같은 방법도 있다.

<br>

## 인덱스를 이용해 배열 요소 접근

```java
a1 = arr[1]

// 값을 가져올 때
int[] temp = new int[] {1,2,3,4,5,6,7};
		for (int i = 0; i < temp.length; i++) {
			System.out.println("arr[" + i + "] : " + temp[i]);
		}
// 값을 저장할 때
int[] temp2 = new int[5];
		for (int i = 0; i < temp2.length; i++) {
			temp2[i] = i + 1;
			System.out.println("arr[" + i + "] : " + temp2[i]);
		}
```

- 배열의 요소에 접근할 때는 `배열이름[index]`에서 원하는 인덱스 번호를 넣으면 그 배열의 요소에 접근할 수 있다. 참고로 자바에서 배열 인덱스는 0부터 시작한다.
- 배열을 사용할 때는 일반적으로 반복문을 사용해서 값을 꺼내오거나 저장하는게 편하다.

<br>

## 배열 복사(Array Copy)

![](https://help.perforce.com/sourcepro/11.1/html/toolsug/images/copy_bag_2.gif)

<center>shallow copy vs deep copy</center>

<br>

- 배열 복사에 대해 알기전에 우선 shallow 와 deep 한 copy의 차이를 짚고 가야한다.
- 배열은 객체는 아니지만 참조 자료형이기 때문에 원시 데이터를 복사할 때랑 같은 방식으로 작동하지는 않는다.
- **얕은 복사(shallow copy)** : 주소값만 가져와 복사하기 때문에 결국 같은 곳을 가리킨다.
- **깊은 복사(deep copy)** : 실제 배열 안의 데이터를 가져와 새로운 배열에 복사한다.

```java
// shallow copy
int[] arr = {1,2,3};
int[] arr2 = arr;
arr2[0] = 10;

// deep copy
int[] arr3 = new int[3];
		for (int i = 0; i < 3; i++) {
			arr3[i] = arr[i];
		}
```

<br>

코드를 보면 위쪽 경우에는 원래 배열 arr의 주소값만 arr2에 복사해 담는 것이기 때문에 결국에는 arr과 arr2는 "같은 배열을 가리키는 것"을 알 수 있다. arr과 arr2에 담기는 것은 배열의 실제 데이터가 아니라 "주소값"이라는 것을 명심하자.

따라서 진짜 배열의 데이터를 "복제"하고 싶다면 아래와 같이 배열의 인덱스를 통해 실제 데이터 값에 접근해서 그걸 새로운 배열의 인덱스를 통해 넣어주면 되는 것이다.

## 배열이 중요한 이유!

사실 처음 자바를 공부했을 때는 배열에 대해서는 중요하게 생각하지 않고 넘어갔던 것 같다. 그렇지만 배열은 자료구조를 공부함에 있어서 제일 기본적인 구조이고 이걸 바탕으로 다양하고 복잡한 자료구조가 생겨나기 때문에 (예를 들면, 벡터, 스택이나 큐 같은 자료구조도 배열로 구현할 수 있다고 한다.) 제대로 이해하고 가야겠다.

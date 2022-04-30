---
emoji: 🪤
title: 자바 Collection Framework
date: '2022-03-22 21:11:00'
author: bontaedev
tags: java webdev study
categories: java
---

> ## 자바 컬렉션 프레임워크

- 컬렉션(Collection) : 여러가지 종류의 객체를 모아놓은 것
- 프레임워크(Framework) : 표준화, 정형화 된 체계적인 프로그래밍 방식
- Collection Framework : 다수의 데이터를 효과적으로 처리하기 위해서 표준화된 방법을 제공하는 클래스 들의 집합
- JDK 1.2부터 제공

## 컬렉션 프레임워크의 주요 인터페이스

- List / Map / Set

  - List : 순서가 있는 데이터의 집합. 중복허용
  - Set : 순서를 유지하지 않는 데이터의 집합. 중복허용x
  - Map : key-value 쌍으로 이루어진 데이터의 집합. 순서는 유지되지 않음. 키는 중복x 값은 중복o

  ## 컬렉션 인터페이스의 메서드

  1. Collection 인터페이스

  - 추가 : boolean add(Object o), boolean addAll(Collection c)
  - void clear()
  - 검색 : boolean contains(Object o), boolean containsAll(Collection c)
  - 삭제 : boolean remove(Object o), boolean removeAll(Collection c),
    boolean retainAll(Collection c)
  - int size()

2. List 인터페이스

## ArrayList (배열기반)

- 기존의 Vector를 개선한 것으로 구현원리와 기능적으로 동일
- Vector는 자체적으로 동기화처리가 되나 ArrayList는 안됨
- List인터페이스를 구현하여 순서가 있고, 중복o
- 데이터의 저장공간으로 배열을 사용 (배열 기반)

```java
// ArrayList 생성
    ArrayList list1 = new ArrayList(10);
		list1.add(new Integer(5));
		list1.add(new Integer(4));
		list1.add(new Integer(2));
		list1.add(new Integer(0));
		list1.add(new Integer(1));
		list1.add(new Integer(3));
// list1의 일부를 가지고 새로운 리스트 생성
		ArrayList list2 = new ArrayList(list1.subList(1,4));
		print(list1, list2);

		Collections.sort(list1);	// list1과 list2를 정렬한다.
		Collections.sort(list2);	// Collections.sort(List l)
		print(list1, list2);

		System.out.println("list1.containsAll(list2):" + list1.containsAll(list2));

		list2.add("B");
		list2.add("C");
		list2.add(3, "A");
		print(list1, list2);

		list2.set(3, "AA");
		print(list1, list2);

		// list1에서 list2와 겹치는 부분만 남기고 나머지는 삭제한다.
		System.out.println("list1.retainAll(list2):" + list1.retainAll(list2));
		print(list1, list2);

		//  list2에서 list1에 포함된 객체들을 삭제한다.
		for(int i= list2.size()-1; i >= 0; i--) {
			if(list1.contains(list2.get(i)))
				list2.remove(i);
		}
		print(list1, list2);
```

## LinkedList

- 배열의 장단점: 배열은 구조가 간단, 접근시간이 짧다. 데이터가 연속적
- 한번 생성하면 크기변경 불가 (새로 배열을 만들고 / 기존내용 복사 / 참조변경 해야 함)
- 비순차적(중간에) 데이터의 추가, 삭제 시에 시간이 많이 걸림

- LinkedList : 배열의 단점을 보완
- 비순차적으로 데이터를 추가삭제 해도 빠르다.
- 배열과 달리 LinkedList는 `불연속적`으로 존재하는 데이터를 연결

- 데이터 삭제: 단 한번의 참조변경으로 가능 (연결이 끊긴 노드는 gc가 처리)
- 데이처 추가: 한번의 node객체 생성과 두번의 참조 변경으로 가능
- 단점 : 데이터 접근성이 나쁨. 데이터 접근 시간은 ArrayList가 빠르다
- 이를 보완한 Doubly LinkedList(이중연결리스트) - 접근성 향상),
- Doubly Circular Linked List : 이중연결리스트에서 마지막 요소와 첫번째 요소를 연결시킨 것

정리

- 순차적으로 추가/삭제하는 경우에는 ArrayList가 LinkedList보다 빠르다
- 중간 데이터를 추가/삭제하는 경우에는 LinkedList가 Array보다 빠르다

## Stack & Queue

- Stack : LIFO(LastInFirstOut) 구조 / 마지막 저장을 제일먼저 out
- Queue: FIFO(FirstInFirstOut) 구조 / 제일먼저 저장을 제일먼저 out

- Stack : 순차적으로 데이터 추가 삭제. ArrayList로 구성
- Queue : 데이터의 추가 삭제가 쉬운 LinkedList로 구현

스택과 큐의 활용

- 스택의 활용 예 : 수식계산, 수식괄호검사, 뒤로가기 기능
- 큐의 활용 예 : 최근사용문서, 인쇄작업 대기 목록, 버퍼

## Iterator, ListIterator, Enumeration, Map

- 컬렉션에 저장된 데이터를 접근하는데 사용하는 인터페이스
- 컬렉션에 저장된 요소를 읽어오는 방법을 표준화해서 접근하기 쉽도록 한다
- Enumeration은 Iteration의 구버전
- ListIterator는 Iterator에서 양방향으로 접근성을 향상시킨 것이다
- 컬렉션에 iterator()를 호출하여 iterator를 구현한 인스턴스(일회용)를 얻어서 사용한다.
- Object next() : 다음 요소를 읽어온다. / boolean hasNext() : 다음에 읽어올 요소가 있는지 확인

```java
ArrayList list = new ArrayList();
		list.add("1");
		list.add("2");
		list.add("3");
		list.add("4");
		list.add("5");

		Iterator it = list.iterator();

		while(it.hasNext()) {
			Object obj = it.next();
			System.out.println(obj);
    }
```

## Arrays

- 배열을 다루는데 유용한 메서드를 정의해놓은 클래스
- copyOf(), copyOfRange() : 배열의 일부, 전체를 복사해 새로운 배열을 반환
- fill() : 배열의 모든 요소를 지정된 값으로 채운다
- setAll() : 배열을 채우는데 사용할 함수형 인터페이스를 매개변수로 받는다.
- sort(), binarySearch() : 배열을 정렬할 때, 배열에 저장된 요소를 이진탐색으로 검색할 때.
- equals(), toString() : 배열의 모든 요소를 출력할 수 있다. 일차원 배열에만 사용
- deepToString() : 다차원 배열의 출력
- asList(Object... a) : 배열을 List에 담아서 반환한다. 매개변수로 가변인수로 나열했을 때도 가능하다.

## Comparator, Comparable

- 컬렉션을 정렬하는데 필요한 메서드 들을 정의하는 인터페이스

```java

```

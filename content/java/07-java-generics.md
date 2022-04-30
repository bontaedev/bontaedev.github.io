---
emoji: 🪤
title: 자바 지네릭스 (Generics)
date: '2022-03-22 21:11:00'
author: bontaedev
tags: java webdev study
categories: java
---

## 제네릭 Generics

- 데이터 형식에 의존하지 않고, 하나의 값이 여러가지 다른 데이터 타입을 가질 수 있도록 하는 방법.
- 예를 들어, 우리가 어떤 자료구조를 만들어 배포하고 싶다고 하자, 그런데 지원하고 싶은 데이터가 String, Integer등 여러 가지 타입을 지원하고 싶을 때 제너릭을 사용한다.
- 정확하게는 컴파일 시 타입을 체크해주는 기능이다. (JDK 1.5)
- 사용자의 필요에 의해 타입을 지정

## 제네릭의 장점

- 잘못된 타입이 들어올 수 있는 것을 컴파일 레벨에서 방지할 수 있다.
- 타입 안정성 제공 : 클래스 외부에서 타입을 지정하므로 따로 타입을 체크하고 형변환할 필요가 없다.
- 비슷한 기능을 지원하는 경우 코드의 재사용성이 높아진다.
- ClassCastException(형변환에러)를 줄이고 코드를 간결하게 함
- 타입을 미리 추론해 런타임에서 발생하는 에러를 컴파일에러로 해결할 수 있도록 해준다.

```java
import java.util.ArrayList;

public class GenericList {
	public static void main(String[] args) {
		ArrayList<Object> list = new ArrayList<Object>();
		list.add(10); // autoboxing
		list.add(20);
		list.add("30"); // 타입체크가 강화

		Integer i = (Integer)list.get(2);
		//컴파일 할때는 문제가 없었는데 실행할때 컴파일 에러

		String i = (String)list.get(2);

		System.out.println(list);
	}
}
```

위의 경우에 ArrayList에서 제너릭을 사용해 Object형 데이터만 다루도록 지정하고 있다. add를 통해 첫번째, 두번째 요소는 오토박싱으로 형변환되서 문제없이 추가되지만 세번째 요소부터는 에러가 발생

## 타입변수 T

- 클래스를 작성할 때 Object 대신 T를 선언하여 사용
- 객체를 new로 생성할 때 타입변수 대신 실제 타입을 대입
- 타입 변수 대신 실제 타입이 지정되면, 형변환을 생략할 수 있음

```java
import java.util.ArrayList;

class Tv {}
class Audio {}

public class GenericList {
	public static void main(String[] args) {
		ArrayList list = new ArrayList();
		ArrayList<Tv> list2 = new ArrayList<Tv>();
    // Tv타입의 객체만 저장가능
		list.add(new Tv());
		// list.add(new Audio()); 에러

		// Tv t = (Tv)list.get(0); 옛날 형변환필요
		Tv t = list2.get(0); // 형변환 불필요(타입일치)
	}
}
```

## 원시타입

## 지네릭과 다형성

- 참조변수와 생성자의 대입된 타입은 일치해야 한다

```java
ArrayList<Tv> list = new ArrayList<Tv>();
```

- 지네릭 클래스 끼리의 다형성은 성립

```java
List<Tv> list = new ArrayList<Tv>();
List<Tv> list = new LinkedList<Tv>();
```

- 매개변수의 다형성도 성립

```java
ArrayList<Product> list = new ArrayList<Product>();
list.add(new Product());
list.add(new Tv()); // 가능
list.add(new Audio()); // 가능
```

## 와일드카드 <?>

- 하나의 참조변수로 대입된 타입이 다른 객체를 참조할 수 있다.

```java
ArrayList<? extends Product> list // Product와 그 자손들만 가능
ArrayList<? extends super T> list // T와 그 조상들만 가능
ArrayList<?> list // 제한없음 모든 타입 가능 <? extends Object>
```

## 제너릭 메서드

- Generic 타입이 선언된 메서드 (타입변수는 메서드 내에서만 유효)
- 메서드를 호출할 때마다 타입을 대입한다.
- 와일드카드는 하나의 참조변수로 서로 다른 타입이 대입된 여러 객체를 다루기 위함
- generic 메서드

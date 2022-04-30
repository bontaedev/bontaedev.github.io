---
emoji: 🪤
title: 자바 객체지향 프로그래밍 정리 - 오버로딩
date: '2022-03-15 22:21:00'
author: bontaedev
tags: java webdev study
categories: java
---

> ## 자바 객체지향 프로그래밍과 관련된 부분을 학습하고 정리한 포스트입니다.

# 오버라이딩(overriding)

- 조상 클래스로부터 상속받은 메서드의 내용을 변경하는 것
- 조건 : 이름 / 매개변수 / 반환타입 이 같아야 한다. (선언부)
- 접근제어자와 예외는 제한된 조건에서 변경가능

  - 조상클래스보다 넓거나 같게는 변경가능 (ex. protected -> public / protected )
  - 조상클래스보다 많은 예외를 등록할 수 없다.
  - 인스턴스 메서드를 static 메서드 또는 반대로 변경할 수 없음

  ```java
  Class Parent {
    void parentMethod() throws IOException, SQLException {
      ...
    }
  }

  Class Child extends Parent {
    void parentMethod() throws IOException {
      ...
    }
  }
  // 자식 클래스에서 더 많은 예외를 던질 수 없다. (x)
  ```

## 오버로딩 vs 오버라이딩

- overloading : 기존에 없는 새로운 메서드를 정의
- overriding : 상속받은 메서드의 내용을 변경

```java
class Parent {
  void parentMethod() {}
}

class Child extends Parent {
  void parentMethod() {} // overriding
  void parentMethod(int i) {} // overloading

  void childMethod() {}
  void childMethod(int i) {} // overloading
  void childMethod() {} // error!
}
```

## super

- 자손 클래스에서 조상클래스의 상속받은 멤버를 참조하기 위해 사용하는 변수

```java
class

```

## super() - 조상클래스의 생성자

- 조상클래스의 생성자를 자식클래스에서 호출할 때 사용
- 조상클래스의 생성자를 호출하면 자손클래스의 인스턴스에서 조상클래스의 멤버를 사용할 수 있다.
  - 자손의 멤버 + 조상의 멤버 -> 하나의 인스턴스
- Object 클래스를 상속받는 모든 클래스의 생성자의 첫 줄에는 생성자.this() 이나 super()를 호출해야 한다. 안하면 컴파일러가 자동으로 추가한다.

## 제어자 (modifier)

- 클래스, 변수, 메서드의 선언부에 사용되어 부가적인 의미를 부여
- 접근제어자 : public, protected, default, private

1. static (공통적인)

- 공통적으로 사용되는 영역인 static에 생성될 수 있게 지정해줌
- static 멤버변수 : 클래스변수로 지정됨. 클래스가 메모리에 로드되면 생성된다. 즉 인스턴스 없이 사용가능.
- static 메서드 : 인스턴스 생성없이 호출가능하다. 인스턴스 멤버들을 사용할 수는 없다.

```java
class StaticTest {
  static int width = 200; // 클래식 멤버변수
  static int height = 120;

  static { // 클래스 초기화 블럭
    // static변수위 복잡한 초기화 진행
  }

  static int max(int a, int b) { // static 메서드
    retu
  }
}
```

2. final (마지막의)

- 상수를 사용하거나 메서드에 쓰면 오버라이딩을 못하게 하고, 클래스에 사용하면 상속을 제한한다.

```java
final class FinalTest { // 상속 안됨
  final int MAX_SIZE = 10; // 상수
  final void getMaxSize() {
    final int LV = MAX_SIZE;
    return MAX_SIZE;
  }
}

// 생성자를 이용해 final멤버 변수를 초기화
class Card {
  final int NUMBER;
  ...

  Card(Strign kind, int num) { // 생성자로 final 변수 초기화
  KIND = kind;
  NUMBER = num;
}
...

c.NUMBER = 5; // 물론 접근해서 새로운 값을 할당할 수는 없다!
}

```

3. abstract (추상)

- 메서드의 선언부만 작성하고 실제 수행내용은 수행하지 않음
- 추상클래스, 추상메서드를 작성할 때 사용

4. 접근제어자

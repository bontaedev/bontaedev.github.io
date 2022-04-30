---
emoji: 👀
title: 자바 입출력 정리
date: '2022-03-22 22:21:00'
author: bontaedev
tags: java webdev study
categories: java
---

> ## 자바의 입출력과 관련된 부분을 학습하고 정리한 포스트입니다.

## 파일 입출력

- 파일을 객체로(인스턴스화) 만들어 사용
- 파일 생성자의 인자값 : HDD에서 해당 파일의 경로값, + 파일명 + 확장자
- 파일을 다룰 때 주의할 점 : 파일의 확장자까지 이름에 속한다.

<br>

## 스트림(Stream)

- 스트림 : 입력장치와 출력장치 사이에 데이터가 흐르는 통로
- 입력한 데이터는 입력 스트림을 통해 컴퓨터로 전달되고 출력스트림을 통해 출력장치로 전달된다.
- 파일은 입력 스트림을 통해 데이터로 프로그램으로 전달된다.
- 프로그램은 출력 스트림을 통해 데이터를 내보낸다.

<br><br>

## try ~ catch 구문

- try ~ with resource : try문이 끝나면 객체를 자동으로 반납할 수 있게 처리
- try ~ catch ~ finally : finally문은 catch문에서 잡지 못한 나머지 예외를 잡기 위한 공간

```java

// try ~ resource
try(FileInputStream fis = new FileInputStream("test.txt")) {

    // 예외를 잡고 싶은 부분

		} catch (Exception e) {
			e.printStackTrace();
		}

// try catch finally
FileInputStream fis = null;
		try {
			// 파일과 관련된 객체 인스턴스를 만들었을 때는 객체 반납을 마지막에 해줘야 함!
			fis = new FileInputStream("test.txt");

		} catch (Exception e) {
			e.printStackTrace();
		} finally { // try 문에서 아무리 예외가 발생해도 마지막으로 잡아주는 곳
			try {
				fis.close();
			} catch (Exception e2) {
				e2.printStackTrace();
			}
		}
```

<br><br>

## 입출력 관련 메서드

- File클래스에 정의되어 있는 메서드들

```java
File file = new File("test.txt");
		System.out.println("이 파일이 실제로 존재하는가? " + file.exists());
		System.out.println("파일인가? " + file.isFile());
		System.out.println("디렉토리인가? " + file.isDirectory());
		System.out.println("파일의 크기? : " + file.length());
		System.out.println("파일의 절대 경로 : " + file.getAbsolutePath());
		System.out.println("파일의 이름 : " + file.getName());

```

<br>

- 파일 생성 (createNewFile), 디렉터리 생성(mkdir)

```java
File file2 = new File("new.txt");
		if (!file2.exists()) {
			// Checked Exception : 코드가 실제 실행되기도 전에 에러가 발생할 수 있다고 보여지는 에러
			try {
				file2.createNewFile();
			} catch (Exception e) {
				e.printStackTrace();
			}
		}

		File newFolder = new File("newfolder");
		if (!newFolder.exists()) {
			newFolder.mkdir();
		}
```

<br><br>

## 파일 입출력 스트림

### 파일 입력 스트림 (FileInputStream, FileReader)

파일 -> 프로그램

- FileInputStream (byte단위로 읽기)

```java
try(FileInputStream fis = new FileInputStream("test.txt")) {

			/*
			System.out.println((char)fis.read()); // 파일의 첫글자를 Ascii코드로 읽어옴 (a=97)
			*/

			// 데이터를 한번에 읽어오기.
			// test.txt 로부터 읽어들여온 데이터를 fileContents 배열안에 모두 담아준다.
			byte[] fileContents = new byte[100];
			fis.read(fileContents);

			for (byte b : fileContents) {
				System.out.print((char)b + " ");
			}

			// 스트링을 이용하는 출력하는 방법
			System.out.println(new String(fileContents));

		} catch (Exception e) {
			e.printStackTrace();
		}
```

<br>

- FileReader (character 단위로 읽기)
  - BufferedReader : 데이터를 한 줄 단위로 읽어올 수 있게 한다.
  - readLine이 실행될 때마다 한 줄씩 내려감

```java
try (FileReader fr = new FileReader("test.txt");
			BufferedReader br = new BufferedReader(fr);) {
// 한글자 씩 읽기
//			System.out.println((char)fr.read());
//			System.out.println((char)fr.read());
//			System.out.println((char)fr.read());
// 한 줄씩 읽기
//			System.out.println(br.readLine());
//			System.out.println(br.readLine());
			String line = "";

			while ((line = br.readLine()) != null) { // 라인이 비어있을 때까지 반복
				System.out.println(line);
			}

		} catch (IOException e) {
			e.printStackTrace();
		}
```

<br>

### 파일 출력 스트림 (FileOutputStream, FileWriter)

프로그램 - 파일

- write은 이미 존재하는 파일에 쓰는 역할이고, 파일생성은 FileOutputStream 객체의 인스턴스가 생성될 때 생성한다.
- 이 프로그램은 실행할 때마다 인스턴스를 생성하니까 파일이 덮어씌워진다.
- 기존 파일에 이어서 내용을 작성하고 싶다면? FileOutputStream에 true 인자값을 추가
- flush() : 입력된 내용을 마지막에 한번에 밀어줄 때 사용.

<br>

- FileOutputStream (byte 단위)

```java
try (FileOutputStream fos = new FileOutputStream("output.txt", true)) {
			byte[] fileContents = {'a','b','c','d'};
			fos.write(fileContents);

		} catch (IOException e) {
			e.printStackTrace();
		}
```

<br>

- FileWriter (character 단위)

```java
String sampleStr = "..."

		try (FileWriter fw = new FileWriter("newKorean.txt")) {
			// String 값을 그대로 넘겨줄 수 있음!
			fw.write(sampleStr);
			fw.flush();

		} catch (IOException e) {
			e.printStackTrace();
		}
```

```toc

```

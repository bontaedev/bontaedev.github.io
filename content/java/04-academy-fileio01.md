---
emoji: ๐
title: ์๋ฐ ์์ถ๋ ฅ ์ ๋ฆฌ
date: '2022-03-22 22:21:00'
author: bontaedev
tags: java webdev study
categories: java
---

> ## ์๋ฐ์ ์์ถ๋ ฅ๊ณผ ๊ด๋ จ๋ ๋ถ๋ถ์ ํ์ตํ๊ณ  ์ ๋ฆฌํ ํฌ์คํธ์๋๋ค.

## ํ์ผ ์์ถ๋ ฅ

- ํ์ผ์ ๊ฐ์ฒด๋ก(์ธ์คํด์คํ) ๋ง๋ค์ด ์ฌ์ฉ
- ํ์ผ ์์ฑ์์ ์ธ์๊ฐ : HDD์์ ํด๋น ํ์ผ์ ๊ฒฝ๋ก๊ฐ, + ํ์ผ๋ช + ํ์ฅ์
- ํ์ผ์ ๋ค๋ฃฐ ๋ ์ฃผ์ํ  ์  : ํ์ผ์ ํ์ฅ์๊น์ง ์ด๋ฆ์ ์ํ๋ค.

<br>

## ์คํธ๋ฆผ(Stream)

- ์คํธ๋ฆผ : ์๋ ฅ์ฅ์น์ ์ถ๋ ฅ์ฅ์น ์ฌ์ด์ ๋ฐ์ดํฐ๊ฐ ํ๋ฅด๋ ํต๋ก
- ์๋ ฅํ ๋ฐ์ดํฐ๋ ์๋ ฅ ์คํธ๋ฆผ์ ํตํด ์ปดํจํฐ๋ก ์ ๋ฌ๋๊ณ  ์ถ๋ ฅ์คํธ๋ฆผ์ ํตํด ์ถ๋ ฅ์ฅ์น๋ก ์ ๋ฌ๋๋ค.
- ํ์ผ์ ์๋ ฅ ์คํธ๋ฆผ์ ํตํด ๋ฐ์ดํฐ๋ก ํ๋ก๊ทธ๋จ์ผ๋ก ์ ๋ฌ๋๋ค.
- ํ๋ก๊ทธ๋จ์ ์ถ๋ ฅ ์คํธ๋ฆผ์ ํตํด ๋ฐ์ดํฐ๋ฅผ ๋ด๋ณด๋ธ๋ค.

<br><br>

## try ~ catch ๊ตฌ๋ฌธ

- try ~ with resource : try๋ฌธ์ด ๋๋๋ฉด ๊ฐ์ฒด๋ฅผ ์๋์ผ๋ก ๋ฐ๋ฉํ  ์ ์๊ฒ ์ฒ๋ฆฌ
- try ~ catch ~ finally : finally๋ฌธ์ catch๋ฌธ์์ ์ก์ง ๋ชปํ ๋๋จธ์ง ์์ธ๋ฅผ ์ก๊ธฐ ์ํ ๊ณต๊ฐ

```java

// try ~ resource
try(FileInputStream fis = new FileInputStream("test.txt")) {

    // ์์ธ๋ฅผ ์ก๊ณ  ์ถ์ ๋ถ๋ถ

		} catch (Exception e) {
			e.printStackTrace();
		}

// try catch finally
FileInputStream fis = null;
		try {
			// ํ์ผ๊ณผ ๊ด๋ จ๋ ๊ฐ์ฒด ์ธ์คํด์ค๋ฅผ ๋ง๋ค์์ ๋๋ ๊ฐ์ฒด ๋ฐ๋ฉ์ ๋ง์ง๋ง์ ํด์ค์ผ ํจ!
			fis = new FileInputStream("test.txt");

		} catch (Exception e) {
			e.printStackTrace();
		} finally { // try ๋ฌธ์์ ์๋ฌด๋ฆฌ ์์ธ๊ฐ ๋ฐ์ํด๋ ๋ง์ง๋ง์ผ๋ก ์ก์์ฃผ๋ ๊ณณ
			try {
				fis.close();
			} catch (Exception e2) {
				e2.printStackTrace();
			}
		}
```

<br><br>

## ์์ถ๋ ฅ ๊ด๋ จ ๋ฉ์๋

- Fileํด๋์ค์ ์ ์๋์ด ์๋ ๋ฉ์๋๋ค

```java
File file = new File("test.txt");
		System.out.println("์ด ํ์ผ์ด ์ค์ ๋ก ์กด์ฌํ๋๊ฐ? " + file.exists());
		System.out.println("ํ์ผ์ธ๊ฐ? " + file.isFile());
		System.out.println("๋๋ ํ ๋ฆฌ์ธ๊ฐ? " + file.isDirectory());
		System.out.println("ํ์ผ์ ํฌ๊ธฐ? : " + file.length());
		System.out.println("ํ์ผ์ ์ ๋ ๊ฒฝ๋ก : " + file.getAbsolutePath());
		System.out.println("ํ์ผ์ ์ด๋ฆ : " + file.getName());

```

<br>

- ํ์ผ ์์ฑ (createNewFile), ๋๋ ํฐ๋ฆฌ ์์ฑ(mkdir)

```java
File file2 = new File("new.txt");
		if (!file2.exists()) {
			// Checked Exception : ์ฝ๋๊ฐ ์ค์  ์คํ๋๊ธฐ๋ ์ ์ ์๋ฌ๊ฐ ๋ฐ์ํ  ์ ์๋ค๊ณ  ๋ณด์ฌ์ง๋ ์๋ฌ
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

## ํ์ผ ์์ถ๋ ฅ ์คํธ๋ฆผ

### ํ์ผ ์๋ ฅ ์คํธ๋ฆผ (FileInputStream, FileReader)

ํ์ผ -> ํ๋ก๊ทธ๋จ

- FileInputStream (byte๋จ์๋ก ์ฝ๊ธฐ)

```java
try(FileInputStream fis = new FileInputStream("test.txt")) {

			/*
			System.out.println((char)fis.read()); // ํ์ผ์ ์ฒซ๊ธ์๋ฅผ Ascii์ฝ๋๋ก ์ฝ์ด์ด (a=97)
			*/

			// ๋ฐ์ดํฐ๋ฅผ ํ๋ฒ์ ์ฝ์ด์ค๊ธฐ.
			// test.txt ๋ก๋ถํฐ ์ฝ์ด๋ค์ฌ์จ ๋ฐ์ดํฐ๋ฅผ fileContents ๋ฐฐ์ด์์ ๋ชจ๋ ๋ด์์ค๋ค.
			byte[] fileContents = new byte[100];
			fis.read(fileContents);

			for (byte b : fileContents) {
				System.out.print((char)b + " ");
			}

			// ์คํธ๋ง์ ์ด์ฉํ๋ ์ถ๋ ฅํ๋ ๋ฐฉ๋ฒ
			System.out.println(new String(fileContents));

		} catch (Exception e) {
			e.printStackTrace();
		}
```

<br>

- FileReader (character ๋จ์๋ก ์ฝ๊ธฐ)
  - BufferedReader : ๋ฐ์ดํฐ๋ฅผ ํ ์ค ๋จ์๋ก ์ฝ์ด์ฌ ์ ์๊ฒ ํ๋ค.
  - readLine์ด ์คํ๋  ๋๋ง๋ค ํ ์ค์ฉ ๋ด๋ ค๊ฐ

```java
try (FileReader fr = new FileReader("test.txt");
			BufferedReader br = new BufferedReader(fr);) {
// ํ๊ธ์ ์ฉ ์ฝ๊ธฐ
//			System.out.println((char)fr.read());
//			System.out.println((char)fr.read());
//			System.out.println((char)fr.read());
// ํ ์ค์ฉ ์ฝ๊ธฐ
//			System.out.println(br.readLine());
//			System.out.println(br.readLine());
			String line = "";

			while ((line = br.readLine()) != null) { // ๋ผ์ธ์ด ๋น์ด์์ ๋๊น์ง ๋ฐ๋ณต
				System.out.println(line);
			}

		} catch (IOException e) {
			e.printStackTrace();
		}
```

<br>

### ํ์ผ ์ถ๋ ฅ ์คํธ๋ฆผ (FileOutputStream, FileWriter)

ํ๋ก๊ทธ๋จ - ํ์ผ

- write์ ์ด๋ฏธ ์กด์ฌํ๋ ํ์ผ์ ์ฐ๋ ์ญํ ์ด๊ณ , ํ์ผ์์ฑ์ FileOutputStream ๊ฐ์ฒด์ ์ธ์คํด์ค๊ฐ ์์ฑ๋  ๋ ์์ฑํ๋ค.
- ์ด ํ๋ก๊ทธ๋จ์ ์คํํ  ๋๋ง๋ค ์ธ์คํด์ค๋ฅผ ์์ฑํ๋๊น ํ์ผ์ด ๋ฎ์ด์์์ง๋ค.
- ๊ธฐ์กด ํ์ผ์ ์ด์ด์ ๋ด์ฉ์ ์์ฑํ๊ณ  ์ถ๋ค๋ฉด? FileOutputStream์ true ์ธ์๊ฐ์ ์ถ๊ฐ
- flush() : ์๋ ฅ๋ ๋ด์ฉ์ ๋ง์ง๋ง์ ํ๋ฒ์ ๋ฐ์ด์ค ๋ ์ฌ์ฉ.

<br>

- FileOutputStream (byte ๋จ์)

```java
try (FileOutputStream fos = new FileOutputStream("output.txt", true)) {
			byte[] fileContents = {'a','b','c','d'};
			fos.write(fileContents);

		} catch (IOException e) {
			e.printStackTrace();
		}
```

<br>

- FileWriter (character ๋จ์)

```java
String sampleStr = "..."

		try (FileWriter fw = new FileWriter("newKorean.txt")) {
			// String ๊ฐ์ ๊ทธ๋๋ก ๋๊ฒจ์ค ์ ์์!
			fw.write(sampleStr);
			fw.flush();

		} catch (IOException e) {
			e.printStackTrace();
		}
```

```toc

```

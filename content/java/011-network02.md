---
emoji: ๐ชค
title: ์๋ฐ ๋คํธ์ํฌ ํ๋ก๊ทธ๋๋ฐ 02
date: '2022-03-25 21:13:00'
author: bontaedev
tags: java webdev study
categories: java
---

> # ์๋ฐ์์ ๋คํธ์ํฌ ํํธ๋ฅผ ํ์ตํ๊ณ  ์ ๋ฆฌํ ๋ด์ฉ์๋๋ค.

- ํด๋ผ์ด์ธํธ ์์ผ ์์ฑ
- ์์ผ ๊ฐ์ฒด ์์ฑ์ ์ธ์๊ฐ ํ์ (์๋ฒ์ IP, ์๋ฒ์์ ์ด์ด์ค ํ๋ก์ธ์ค์ ํฌํธ๋ฒํธ)
- ๋ณธ์ธ์ IP์ฃผ์๋ localhost๋ก ์ ์ด์ค ์ ์๋ค.

```java
// client side
		try (Socket client = new Socket("localhost",8000);) {

		} catch (Exception e) {
			e.printStackTrace();
		}
```

<br>

- ์๋ฒ์ฉ ์์ผ์ ์์ฑ
- ServerSocket : client ์๋งํผ socket์ ์์ฑํด์ฃผ๋ ๊ณต์ฅ
- accept ๋ฉ์๋๋ฅผ ํตํด ํด๋ผ์ด์ธํธ์ ์์ฒญ์ ์๋ฝํ  '์์ผ ์์ฑ'
- ๋๊ธฐํ๋ค๊ฐ ํด๋ผ์ด์ธํธ๊ฐ '์ค์ ๋ก ์ ์ํด์ ๊ฐ์ง'๋์ ๋ ์์ผ ์์ฑ

```java
// server side
		System.out.println("new client connect");

		try (ServerSocket server = new ServerSocket(8000);
			Socket soc = server.accept();) {

			System.out.println("clinet connect success!");
			System.out.println("Connected IP address : " + soc.getLocalAddress());

		} catch (Exception e) {
			e.printStackTrace();
		}
```

## ์ฑํ ํ๋ก๊ทธ๋จ ๊ตฌํํ๊ธฐ

์ฐ์  ํ๋ก๊ทธ๋จ์ด ๋์๊ฐ๋ ๊ณผ์ ์ ์ ๋ฆฌํด๋ณด์.

1. ์๋ฒ๋ฅผ ๊ฐ๋์ํค๊ณ  - ํด๋ผ์ด์ธํธ๊ฐ ์ ์
2. ํด๋ผ์ด์ธํธ์ ํ์์ธ์ฌ ์ ์ก
3. ํด๋ผ์ด์ธํธ๊ฐ ๋๋ค์ ์๋ ฅํ๊ณ  ์ ์ก
4. ์๋ฒ์์ "~๋ ์ ์ํ์์ต๋๋ค" ๋ฉ์ธ์ง ์ ์ก
5. ํด๋ผ์ด์ธํธ๊ฐ ๋จผ์  ๋ฉ์ธ์ง ์ ์ก
6. ์๋ฒ์์ ๋ฉ์ธ์ง๋ฅผ ๋ฐ์ "~๋ ๋ฉ์ธ์ง : ๋ฉ์ธ์ง ๋ด์ฉ" ๋ด์ฉ ์ถ๋ ฅ
7. ์๋ฒ๊ฐ ํด๋ผ์ด์ธํธ์๊ฒ ๋ฉ์ธ์ง ์ ์ก
8. ํด๋ผ์ด์ธํธ๊ฐ ๋ฉ์ธ์ง๋ฅผ ๋ฐ์ "์๋ฒ ๋ฉ์ธ์ง : ๋ฉ์ธ์ง ๋ด์ฉ"์ ์ถ๋ ฅ

- ์๋ฒ์ชฝ ์ฝ๋

```java
Scanner sc = new Scanner(System.in);

		System.out.println("server start!");
		try (ServerSocket server = new ServerSocket(8000);
				Socket soc = server.accept();
				DataInputStream din = new DataInputStream(soc.getInputStream());
				DataOutputStream dout  = new DataOutputStream(soc.getOutputStream());
			) {

			// ํด๋ผ์ด์ธํธ์ ํ์ ๋ฉ์ธ์ง ์๋ ฅํด์ ์ ์ก
			String hi = "์๋ํ์ธ์ welcome to chat!";
			dout.writeUTF(hi);
			dout.flush();

			// ํด๋ผ์์ ์ ์กํ ๋๋ค์ ๋ฐ๊ธฐ
			String nickname = din.readUTF();
			System.out.println(nickname + " ๋ ์ ์ํ์์ต๋๋ค.");

			while (true) {
				// ํด๋ผ์์ ์ ์กํ ๋ฉ์ธ์ง ๋ฐ๊ธฐ
				String receiveMsg = din.readUTF();
				System.out.println(nickname + " ๋ ๋ฉ์์ง : " + receiveMsg);

				// ํด๋ผ๋ก ๋ฉ์ธ์ง ์ ์ก
				System.out.print("๋ฉ์ธ์ง ์๋ ฅ >> ");
				String sendMsg = sc.nextLine();
				dout.writeUTF(sendMsg);
				dout.flush();

			}



		} catch (Exception e) {
			System.out.println("์๋ฒ๋ฅผ ์ฌ๋ถํํ์ธ์.");
			e.printStackTrace();
		}
```

- ํด๋ผ์ด์ธํธ ์ชฝ ์ฝ๋

```java
Scanner sc = new Scanner(System.in);
		try (Socket client = new Socket("localhost",8000);
				DataInputStream din = new DataInputStream(client.getInputStream());
				DataOutputStream dout = new DataOutputStream(client.getOutputStream());
			){

			// ์๋ฒ์์ ๋ณด๋ธ ํ์๋ฉ์ธ์ง ์ถ๋ ฅ
			String hi = din.readUTF();
			System.out.println(hi);

			// ๋๋ค์ ์ ์ก
			System.out.print("๋๋ค์ ์๋ ฅ >> ");
			String nickname = sc.nextLine();
			dout.writeUTF(nickname);
			dout.flush();

			try {
				while (true) {
					// ๋ฉ์ธ์ง ์ ์ก
					System.out.print("๋ฉ์ธ์ง ์๋ ฅ >> ");
					String sendMsg = sc.nextLine();
					dout.writeUTF(sendMsg);
					dout.flush();

					// ์๋ฒ์์ ์ ์กํ ๋ฉ์ธ์ง ๋ฐ๊ธฐ
					String serverMsg = din.readUTF();
					System.out.println("์๋ฒ ๋ฉ์์ง : " + serverMsg);
				}
			} catch (Exception e) {
				System.out.println("์ ์์ด ์ํํ์ง ์์ต๋๋ค. ์ฌ์ ์ํ์ธ์.");
				e.printStackTrace();
			}

		} catch (Exception e) {
			e.printStackTrace();
		}
```

## ๋ก๊ทธ์ธ ๊ธฐ๋ฅ ๊ตฌํ

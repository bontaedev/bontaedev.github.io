---
emoji: 🪤
title: 자바 네트워크 프로그래밍 02
date: '2022-03-25 21:13:00'
author: bontaedev
tags: java webdev study
categories: java
---

> # 자바에서 네트워크 파트를 학습하고 정리한 내용입니다.

- 클라이언트 소켓 생성
- 소켓 객체 생성시 인자값 필요 (서버의 IP, 서버에서 열어준 프로세스의 포트번호)
- 본인의 IP주소는 localhost로 적어줄 수 있다.

```java
// client side
		try (Socket client = new Socket("localhost",8000);) {

		} catch (Exception e) {
			e.printStackTrace();
		}
```

<br>

- 서버용 소켓을 생성
- ServerSocket : client 수만큼 socket을 생성해주는 공장
- accept 메서드를 통해 클라이언트의 요청을 수락할 '소켓 생성'
- 대기하다가 클라이언트가 '실제로 접속해서 감지'됐을 때 소켓 생성

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

## 채팅 프로그램 구현하기

우선 프로그램이 돌아가는 과정을 정리해보자.

1. 서버를 가동시키고 - 클라이언트가 접속
2. 클라이언트에 환영인사 전송
3. 클라이언트가 닉네임 입력하고 전송
4. 서버에서 "~님 접속하였습니다" 메세지 전송
5. 클라이언트가 먼저 메세지 전송
6. 서버에서 메세지를 받아 "~님 메세지 : 메세지 내용" 내용 출력
7. 서버가 클라이언트에게 메세지 전송
8. 클라이언트가 메세지를 받아 "서버 메세지 : 메세지 내용"을 출력

- 서버쪽 코드

```java
Scanner sc = new Scanner(System.in);

		System.out.println("server start!");
		try (ServerSocket server = new ServerSocket(8000);
				Socket soc = server.accept();
				DataInputStream din = new DataInputStream(soc.getInputStream());
				DataOutputStream dout  = new DataOutputStream(soc.getOutputStream());
			) {

			// 클라이언트에 환영 메세지 입력해서 전송
			String hi = "안녕하세요 welcome to chat!";
			dout.writeUTF(hi);
			dout.flush();

			// 클라에서 전송한 닉네임 받기
			String nickname = din.readUTF();
			System.out.println(nickname + " 님 접속하였습니다.");

			while (true) {
				// 클라에서 전송한 메세지 받기
				String receiveMsg = din.readUTF();
				System.out.println(nickname + " 님 메시지 : " + receiveMsg);

				// 클라로 메세지 전송
				System.out.print("메세지 입력 >> ");
				String sendMsg = sc.nextLine();
				dout.writeUTF(sendMsg);
				dout.flush();

			}



		} catch (Exception e) {
			System.out.println("서버를 재부팅하세요.");
			e.printStackTrace();
		}
```

- 클라이언트 쪽 코드

```java
Scanner sc = new Scanner(System.in);
		try (Socket client = new Socket("localhost",8000);
				DataInputStream din = new DataInputStream(client.getInputStream());
				DataOutputStream dout = new DataOutputStream(client.getOutputStream());
			){

			// 서버에서 보낸 환영메세지 출력
			String hi = din.readUTF();
			System.out.println(hi);

			// 닉네임 전송
			System.out.print("닉네임 입력 >> ");
			String nickname = sc.nextLine();
			dout.writeUTF(nickname);
			dout.flush();

			try {
				while (true) {
					// 메세지 전송
					System.out.print("메세지 입력 >> ");
					String sendMsg = sc.nextLine();
					dout.writeUTF(sendMsg);
					dout.flush();

					// 서버에서 전송한 메세지 받기
					String serverMsg = din.readUTF();
					System.out.println("서버 메시지 : " + serverMsg);
				}
			} catch (Exception e) {
				System.out.println("접속이 원활하지 않습니다. 재접속하세요.");
				e.printStackTrace();
			}

		} catch (Exception e) {
			e.printStackTrace();
		}
```

## 로그인 기능 구현

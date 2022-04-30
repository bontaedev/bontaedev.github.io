---
emoji: 🪤
title: 데이터베이스 6일차 정리 - DB 트랜잭션
date: '2022-04-06 23:02:42'
author: bontaedev
tags: database oracle webdev study
categories: database
---

## 트랜잭션이란? Transaction

- 한번에 수행되어야하는 작업 단위
- 하나의 작업을 완료하기 위해서 각각의 흐름의 정상적으로 완료됐을때만 작업단위를 정상적으로 수행되었다고 판단하고 완료하는 과정

- 트랜잭션 예시

ex) ATM

- 1.  카드삽입
- 2.  메뉴 선택(인출)
- 3.  금액확인 / 비밀번호 인증
- 4.  사용자가 입력한 금액이 뽑을 수 있는 금액인지 확인
- 5.  실제 현금 나옴
- 6.  카드 뽑고 끝

```sql
 == 현금을 인출한다 작업
 * -> 6번까지의 작업이 정상적으로 완료가 됐을 때 -> commit(완료 시점)
 * -> 6번까지의 작업 중에 하나라도 비정상 흐름이 발생하면 그때는 모든 작업을 ROLLBACK(취소)
 *
 * commit : 트랜잭션 작업이 정상적으로 완료되면 변경 내용을 영구적으로 저장 (모든 savepoint 삭제)
 * savepoint <savepoint명> : 현재 트랜잭션 작업 시점에다가 이름 부여 (하나의 트린잭션 안에서 구역을 나누는 것)
 *
 * rollback : 트랜잭션 작업을 모두 취소하고 최근에 commit 했던 지점을 돌아가는 것.
 * rollback to savepoint명 : 해당 savepoint로 되돌아간다.
```

```sql
CREATE TABLE tbl_user (
	NO NUMBER UNIQUE
	, id varchar2(100) PRIMARY KEY
	, pw varchar2(100) NOT null
);

INSERT INTO tbl_user values(1,'user1','pw1');
INSERT INTO tbl_user values(2,'user2','pw2');
INSERT INTO tbl_user values(3,'user3','pw3');

SELECT * FROM tbl_user;

COMMIT;

INSERT INTO tbl_user values(4,'user4','pw4');

DELETE FROM tbl_user WHERE NO='4';

ROLLBACK;

INSERT INTO tbl_user values(5,'user5','pw5');
SAVEPOINT sp1;
INSERT INTO tbl_user values(6,'user6','pw6');
SELECT * FROM tbl_user;

rollback TO sp1;
```

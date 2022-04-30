---
emoji: 🪤
title: 데이터베이스 6일차 정리 - 데이터조작어(DML)
date: '2022-04-06 21:21:00'
author: bontaedev
tags: database oracle webdev study
categories: database
---

## 데이터 조작어 DML(Data Manipulation Language)

- Data를 삽입 수정 삭제 조회하는 언어 (CRUD)

# 1. INSERT

> 테이블에 새로은 행을 추가할 때 사용하는 구문

```sql
-- 모든 행에 대한 데이터를 추가하고자 할때 사용하는 구문
INSERT into 테이블명 values (입력할 데이터,...)

-- 특정한 컬럼의 값만 넣고 싶을 때 사용
-- 컬럼과 데이터의 순서는 맞춰줘야 한다.
INSERT INTO 테이블명 (컬럼명1,컬럼명2...) values (입력데이터1,데이터2...)

INSERT INTO MEMBER VALUES ('abc123','abc','ABC초콜릿','abc@naver.com');
INSERT INTO MEMBER (id,pw) VALUES ('eee555', 'eEE');
```

- 서브쿼리를 이용한 INSERT 구문 사용

```sql
INSERT INTO MEMBER
	(SELECT emp_id, job_code, emp_name, email
	FROM employee WHERE emp_id = '200');
```

- 자동형변환(묵시적형변환) : 오라클이 자동으로 자료형을 추측하여 변환해주는 것

```sql
INSERT INTO MEMBER values(123, sysdate,'ffd','abc@naver.com');
```

# 2. UPDATE

> 컬럼에 저장된 데이터를 수정하는 구문. 테이블 전체 행 개수에 변화를 주지 않음

```sql
update 테이블명 SET 변경할 컬럼명 = 변경할 값 ...where 조건

UPDATE MEMBER SET email = 'eee@gmail.com' WHERE id = 'eee555';
UPDATE MEMBER SET pw = '1234', nickname = 'et' WHERE id = 'eee555';
```

# 3. DELETE

> 테이블의 행을 삭제하는 구문. 행의 개수에 변화가 생김
> 조건문을 걸어주지 않으면 테이블의 모든 데이터가 삭제됨

```sql
delete from 테이블명 where 조건...

COMMIT;
SELECT * FROM member;
DELETE FROM MEMBER WHERE id = '200';
DELETE FROM MEMBER;
ROLLBACK;
```

- TRUNCATE : 테이블의 전체 행을 삭제할 때 사용하는 구문. 되돌릴 수 없음, 영구적으로 삭제

`TRUNCATE TABLE MEMBER;`

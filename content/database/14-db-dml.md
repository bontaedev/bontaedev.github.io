---
emoji: ๐ชค
title: ๋ฐ์ดํฐ๋ฒ ์ด์ค 6์ผ์ฐจ ์ ๋ฆฌ - ๋ฐ์ดํฐ์กฐ์์ด(DML)
date: '2022-04-06 21:21:00'
author: bontaedev
tags: database oracle webdev study
categories: database
---

## ๋ฐ์ดํฐ ์กฐ์์ด DML(Data Manipulation Language)

- Data๋ฅผ ์ฝ์ ์์  ์ญ์  ์กฐํํ๋ ์ธ์ด (CRUD)

# 1. INSERT

> ํ์ด๋ธ์ ์๋ก์ ํ์ ์ถ๊ฐํ  ๋ ์ฌ์ฉํ๋ ๊ตฌ๋ฌธ

```sql
-- ๋ชจ๋  ํ์ ๋ํ ๋ฐ์ดํฐ๋ฅผ ์ถ๊ฐํ๊ณ ์ ํ ๋ ์ฌ์ฉํ๋ ๊ตฌ๋ฌธ
INSERT into ํ์ด๋ธ๋ช values (์๋ ฅํ  ๋ฐ์ดํฐ,...)

-- ํน์ ํ ์ปฌ๋ผ์ ๊ฐ๋ง ๋ฃ๊ณ  ์ถ์ ๋ ์ฌ์ฉ
-- ์ปฌ๋ผ๊ณผ ๋ฐ์ดํฐ์ ์์๋ ๋ง์ถฐ์ค์ผ ํ๋ค.
INSERT INTO ํ์ด๋ธ๋ช (์ปฌ๋ผ๋ช1,์ปฌ๋ผ๋ช2...) values (์๋ ฅ๋ฐ์ดํฐ1,๋ฐ์ดํฐ2...)

INSERT INTO MEMBER VALUES ('abc123','abc','ABC์ด์ฝ๋ฆฟ','abc@naver.com');
INSERT INTO MEMBER (id,pw) VALUES ('eee555', 'eEE');
```

- ์๋ธ์ฟผ๋ฆฌ๋ฅผ ์ด์ฉํ INSERT ๊ตฌ๋ฌธ ์ฌ์ฉ

```sql
INSERT INTO MEMBER
	(SELECT emp_id, job_code, emp_name, email
	FROM employee WHERE emp_id = '200');
```

- ์๋ํ๋ณํ(๋ฌต์์ ํ๋ณํ) : ์ค๋ผํด์ด ์๋์ผ๋ก ์๋ฃํ์ ์ถ์ธกํ์ฌ ๋ณํํด์ฃผ๋ ๊ฒ

```sql
INSERT INTO MEMBER values(123, sysdate,'ffd','abc@naver.com');
```

# 2. UPDATE

> ์ปฌ๋ผ์ ์ ์ฅ๋ ๋ฐ์ดํฐ๋ฅผ ์์ ํ๋ ๊ตฌ๋ฌธ. ํ์ด๋ธ ์ ์ฒด ํ ๊ฐ์์ ๋ณํ๋ฅผ ์ฃผ์ง ์์

```sql
update ํ์ด๋ธ๋ช SET ๋ณ๊ฒฝํ  ์ปฌ๋ผ๋ช = ๋ณ๊ฒฝํ  ๊ฐ ...where ์กฐ๊ฑด

UPDATE MEMBER SET email = 'eee@gmail.com' WHERE id = 'eee555';
UPDATE MEMBER SET pw = '1234', nickname = 'et' WHERE id = 'eee555';
```

# 3. DELETE

> ํ์ด๋ธ์ ํ์ ์ญ์ ํ๋ ๊ตฌ๋ฌธ. ํ์ ๊ฐ์์ ๋ณํ๊ฐ ์๊น
> ์กฐ๊ฑด๋ฌธ์ ๊ฑธ์ด์ฃผ์ง ์์ผ๋ฉด ํ์ด๋ธ์ ๋ชจ๋  ๋ฐ์ดํฐ๊ฐ ์ญ์ ๋จ

```sql
delete from ํ์ด๋ธ๋ช where ์กฐ๊ฑด...

COMMIT;
SELECT * FROM member;
DELETE FROM MEMBER WHERE id = '200';
DELETE FROM MEMBER;
ROLLBACK;
```

- TRUNCATE : ํ์ด๋ธ์ ์ ์ฒด ํ์ ์ญ์ ํ  ๋ ์ฌ์ฉํ๋ ๊ตฌ๋ฌธ. ๋๋๋ฆด ์ ์์, ์๊ตฌ์ ์ผ๋ก ์ญ์ 

`TRUNCATE TABLE MEMBER;`

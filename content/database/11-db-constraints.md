---
emoji: ๐ชค
title: ๋ฐ์ดํฐ๋ฒ ์ด์ค 5์ผ์ฐจ ์ ๋ฆฌ - DB_DDL(๋ฐ์ดํฐ์ ์์ด), ์ ์ฝ์กฐ๊ฑด(Constraints)
date: '2022-04-05 20:21:00'
author: bontaedev
tags: database oracle webdev study
categories: database
---

## DDL(Data Definition Language)

- ๋ฐ์ดํฐ ์ ์์ด

### drop : ํ์ด๋ธ์ ์ญ์ ํ๊ธฐ ์ํด ์ฌ์ฉํ๋ ๊ตฌ๋ฌธ

DROP TABLE temp;

### ALTER

- ํ์ด๋ธ์ ์ ์๋ ๋ด์ฉ์ ์์ ํ๊ณ ์ ํ  ๋ ์ฌ์ฉํ๋ ๋ฐ์ดํฐ ์ ์์ด
- ์ปฌ๋ผ ์ถ๊ฐ์ญ์ , ์ ์ฝ์กฐ๊ฑด ์ถ๊ฐ์ญ์ , ์ปฌ๋ผ์ ์๋ฃํ ๋ณ๊ฒฝ, DEFAULT ๊ฐ ๋ณ๊ฒฝ
- ํ์ด๋ธ๋ช,์ปฌ๋ผ๋ช,์ ์ฝ์กฐ๊ฑด์ ์ด๋ฆ ๋ณ๊ฒฝ

```sql
-- ์ด๋ฏธ ์กด์ฌํ๋ ํ์ด๋ธ์ ์๋ก์ด ์ปฌ๋ผ ์ถ๊ฐ
ALTER TABLE MEMBER ADD (name varchar2(100));

-- ์๋ก์ด ์ปฌ๋ผ ์ถ๊ฐ (age) + default
ALTER TABLE MEMBER ADD (age MEMBER DEFAULT 0);

-- ์ ์ฝ์กฐ๊ฑด ์ถ๊ฐ - unique ์ถ๊ฐ
-- ์ถ๊ฐํ  ์ ์ฝ์กฐ๊ฑด์ ์ด๋ฆ๋ ์ง์ด์ค
ALTER TABLE MEMBER ADD constraints id_unq unique(id);

SELECT constraint_name, constraint_type
FROM USER_CONSTRAINTS WHERE TABLE_name = 'MEMBER';

-- ์ ์ฝ์กฐ๊ฑด ์ถ๊ฐ - pw์ปฌ๋ผ์ Not null ์ ์ฝ์กฐ๊ฑด ์ถ๊ฐ
-- add๋ก ์ ๊ทผํ  ์ ์๊ณ  modify๋ก
ALTER TABLE MEMBER ADD CONSTRAINT pw_nn NOT NULL(pw); -- x
ALTER TABLE MEMBER MODIFY pw CONSTRAINT pw_nn NOT NULL;

-- ์ปฌ๋ผ๋ช ์์  - pw ์ปฌ๋ผ์ Password๋ผ๊ณ  ๋ณ๊ฒฝ
ALTER TABLE MEMBER RENAME COLUMN pw TO password;
DESC MEMBER;

-- ์ปฌ๋ผ์ ๋ฐ์ดํฐ ํ์ ์์  - name varchar2(100) -> char(100)
ALTER TABLE MEMBER MODIFY name char(100);

-- ์ปฌ๋ผ์ ์ญ์  (age ์ปฌ๋ผ ์ญ์ )
ALTER TABLE MEMBER DROP COLUMN age;

-- ์ ์ฝ์กฐ๊ฑด ์ญ์  -- password ์ปฌ๋ผ์ ์ ์ฝ์กฐ๊ฑด ์ญ์ 
-- ์ ์ฝ์กฐ๊ฑด์ ์ด๋ฆ์ ๋จผ์  ์์ผ์ผ ํจ
SELECT constraint_name  FROM USER_CONSTRAINTS WHERE table_name='MEMBER';
ALTER TABLE MEMBER DROP CONSTRAINT pw_nn;


-- ์ ์ฝ์กฐ๊ฑด๋ช ์์ 
ALTER TABLE MEMBER RENAME CONSTRAINT SYS_C007112 TO no_pk;

-- ํ์ด๋ธ๋ช ๋ณ๊ฒฝ
ALTER TABLE MEMBER RENAME TO tb1_member;
```

## ์ ์ฝ์กฐ๊ฑด(Constraints)

- ํ์ด๋ธ์ ์์ฑํ  ๋ ๊ตฌ์ฑํ๋ ์ปฌ๋ผ์ ๋ค์ด๊ฐ ๋ฐ์ดํฐ์ ๋ํด ์ ์ฝ์กฐ๊ฑด์ ์ค์ ํ๋ ๊ฒ
- ๋ฐ์ดํฐ์ ์ผ๊ด์ฑ๊ณผ ์ ํ์ฑ์ ์ ์งํ๊ธฐ ์ํด์ (๋ฐ์ดํฐ ๋ฌด๊ฒฐ์ฑ)
  <br>
- `NOT NULL` : ํด๋น ์ปฌ๋ผ์ null ๊ฐ์ด ๋ค์ด๊ฐ ์ ์์.
- `UNIQUE` : ์ค๋ณต๋ ๊ฐ์ ํ์ฉํ์ง ์์
- `Primary Key (๊ธฐ๋ณธํค)` : (NOT NULL + Unique) ๊ณ ์ ํ ์๋ณ์๋ก ์ฌ์ฉํ๋ ์ปฌ๋ผ
- `Foreign Key (์ธ๋ํค)`: ๋ ํ์ด๋ธ ๊ฐ์ ๊ด๊ณ๋ฅผ ์ค์ ํ๊ณ ,
  - bํ์ด๋ธ์ member_id ์ปฌ๋ผ์ ๋ค์ด๊ฐ ์ ์๋ ๊ฐ์ด Aํ์ด๋ธ์ ID์ ์๋ ๋ฐ์ดํฐ์ฌ์ผ ํ๋ ๊ฒฝ์ฐ
  - ์์ /๊ฒ์๊ธ/๋๊ธ ์ ๊ด๊ณ
- `check` : ํด๋น์ปฌ๋ผ์ ์ ์ฅ ๊ฐ๋ฅํ ๊ฐ์ ๋ฒ์ ์กฐ๊ฑด์ ์ง์ ํด์ ์ค์ ํ ๊ฐ๋ง ํ์ฉ

```sql
-- TYPE : P์ด๋ฉด primary key, C์ด๋ฉด Check or not null
SELECT CONSTRAINT_name, CONSTRAINT_type
FROM USER_CONSTRAINTS
	WHERE table_name = 'EMPLOYEE';
```

<br>

- ์ ์ฝ์กฐ๊ฑด์ ๊ฑฐ๋ ์์น (์ปฌ๋ผ๋ ๋ฒจ / ํ์ด๋ธ๋ ๋ฒจ)
  - ์ปฌ๋ผ ๋ ๋ฒจ : ์ปฌ๋ผ๋ช ์๋ฃํ ์์ ์ ์ฝ์กฐ๊ฑด์ ๋ช์ํ๋ ๊ฒฝ์ฐ
  - ํ์ด๋ธ ๋ ๋ฒจ : ์ปฌ๋ผ์ ๋ชจ๋ ์ ์ํ ํ ๋ง์ง๋ง์ ์ ์ฝ์กฐ๊ฑด๋ช ํ์์ผ๋ก ์ ์ฝ์กฐ๊ฑด์ ๊ฑธ์ด์ฃผ๋ ๋ฐฉ์
    <br>

```sql
CREATE TABLE user_cons2(
	NO NUMBER
	, pw varchar2(100) NOT NULL
	, name varchar2(100) NOT NULL
	, gender varchar2(10)
	, UNIQUE(no)
);
```

1. NOT NULL

- Null ๊ฐ์ ํ์ฉX : ํด๋น ์ปฌ๋ผ์ ๋ฐ๋์ ๊ฐ์ด ๊ธฐ๋ก๋์ด์ผ ํ๋ ๊ฒฝ์ฐ

```sql
CREATE TABLE USER_nocons(
	no NUMBER
	, pw varchar2 (100)
	, name varchar2(100)
	, gender varchar2(10)
);
SELECT * FROM user_nocons;
INSERT INTO USER_nocons VALUES (1,'abc123','tom','๋จ');
INSERT INTO USER_nocons VALUES (1,null,null,'์ฌ');

DROP TABLE user_cons;

CREATE TABLE user_cons(
-- ์ปฌ๋ผํ ์๋ฃํ(๊ธธ์ด) ์ ์ฝ์กฐ๊ฑด
	NO NUMBER unique
	, pw varchar2(100) NOT NULL
	, name varchar2(100) NOT NULL
	, gender varchar2(10)
);
SELECT * FROM USER_cons;
INSERT INTO user_cons VALUES (1,'aaa555','paul','๋จ');
INSERT INTO user_cons VALUES (2,NULL,NULL,'์ฌ');
-- ๋ฐ์ดํฐ๋ฅผ ์ฝ์ํ  ๋๋ถํฐ ์ ์ฝ์กฐ๊ฑด์ ๋ถํฉํ์ง ์๋๋ค๋ฉด ๋ฐ์ดํฐ๊ฐ ๋ค์ด๊ฐ์ง ์์
```

2. UNIQUE

- ํด๋น ์ปฌ๋ผ์ ์ค๋ณต๊ฐ์ ์ ํํ๋ ์ ์ฝ์กฐ๊ฑด
- Null๊ฐ๋ ๋ค์ด๊ฐ, ๊ฐ์ ์๋ฃ์ด๋ ๋จ

```sql
-- NO NUMBER unique
SELECT * FROM USER_nocons;
INSERT INTO user_nocons VALUES (1,'eee555','will','๋จ');
INSERT INTO user_cons2 VALUES (1,'asdf','sam','๋จ');
```

3. Primary Key (๊ธฐ๋ณธํค)

- ์ปฌ๋ผ์ ๋ฐ์ดํฐ๊ฐ ๊ณ ์ ํ๊ณ  null์ ํ์ฉํ์ง ์์ (๊ณ ์  ์๋ณ์)
- ํ๋์ ํ์ด๋ธ์์ ํ๋๋ง ๊ฑธ์ด์ค ์ ์๋ค. (๊ณ ์ ์๋ณ์)
- unique + not null ์ ์ฝ์กฐ๊ฑด์ ํ๋์ ํ์ด๋ธ์์๋ ์ฌ๋ฌ๋ฒ ์ฌ์ฉ์ด ๊ฐ๋ฅํ๊ธฐ ๋๋ฌธ์ ์๋ณ์๋ ์๋์ง๋ง ์ค๋ณต๊ฐ๊ณผ NULL์ ์ฒดํฌํ  ๋ ์ฌ์ฉ

```sql
CREATE TABLE user_cons(
	NO NUMBER PRIMARY KEY
	, id varchar2(100) unique NOT NULL
	, pw varchar2(100) NOT NULL
	, nickname varchar2(200) UNIQUE NOT NULL
	, name varchar2(100) NOT NULL
	, gender varchar2(10)
);

INSERT INTO user_cons VALUES (1,'aaa555','paul','๋จ');
INSERT INTO user_cons VALUES (2,'aaa555','paul','๋จ');
```

- primary key์ ๋ํด ํ๋์ ์ปฌ๋ผ์ด ์๋ ์ฌ๋ฌ๊ฐ์ ์ปฌ๋ผ์ ๋ํ ๋ณตํฉํค ํํ๋ก ์ ์ฉ์ ์ํค๊ณ  ์ถ๋ค๋ฉด ์ปฌ๋ผ๋ ๋ฒจ ์์๋ ๋ถ๊ฐ
- ๋ณตํฉํค ํํ๋ก no,id ์ง์ 

```sql
CREATE TABLE user_cons(
	NO NUMBER
	, id varchar2(100)
	, pw varchar2(100)
	, gender varchar2(10)
	, PRIMARY KEY (NO,id)
);
```

4. Foreign Key (์ธ๋ํค) : ์ฐธ์กฐ ๋ฌด๊ฒฐ์ฑ์ ์งํค๊ธฐ ์ํด์

- ์ฐธ์กฐ๋ ๋ค๋ฅธ ํ์ด๋ธ์ด ์ ๊ณตํ๋ ๊ฐ๋ง ์ฌ์ฉํ  ์ ์๋๋ก ์ ์ฝํ๊ณ  ์ถ์ ๋.
- ์ฐธ์กฐํ๋ ์ปฌ๋ผ๊ณผ ์ฐธ์กฐ๋๋ ์ปฌ๋ผ์ ํตํด ๋ ํ์ด๋ธ ๊ฐ์ ๊ด๊ณ๊ฐ ์์ฑ์ด ๋จ.
- ์ฐธ์กฐํ๋ ์ปฌ๋ผ์ด ์ฐธ์กฐ๋๋ ์ปฌ๋ผ์ ์๋ ๊ฐ๊ณผ ์ผ์นํ๊ฑฐ๋, null ๊ฐ๋ง ๊ฐ์ง ์ ์์.
- ์ฐธ์กฐํ๋ ์ปฌ๋ผ : ์ฐธ์กฐ ๋์์ ์ฐธ์กฐํ๋ ํ์ด๋ธ์ ์ปฌ๋ผ (Bํ์ด๋ธ)
- ์ฐธ์กฐ๋๋ ์ปฌ๋ผ : ์ฐธ์กฐ ๋์์ด ๋๋ ํ์ด๋ธ ์ปฌ๋ผ (A*ํ์*ํ์ด๋ธ)

```sql

-- ํ์ ํ์ด๋ธ / ๋์ฌ ํ์ด๋ธ
CREATE TABLE student(
	id varchar2 (100) primary KEY
	, name varchar2 (100) NOT NULL
	, age NUMBER NOT NULL
);

INSERT INTO student VALUES ('001','tom',20);
INSERT INTO student VALUES ('002','cloy',23);
INSERT INTO student VALUES ('003','sally',22);
SELECT * FROM student;

DROP TABLE bookshelf;

CREATE TABLE bookshelf( -- ํ์ด๋ธ๋ ๋ฒจ
	book_id varchar2(100) PRIMARY KEY
	, std_id varchar2(100)
	, rent_date DATE
	, foreign KEY (std_id) REFERENCES student (id)
);

-- foreign key : (์ฐธ์กฐํ๋ ์ปฌ๋ผ) references ์ฐธ์กฐ๋์ํ์ด๋ธ (์ฐธ์กฐ๋์์ปฌ๋ผ)
CREATE TABLE bookshelf( -- ์ปฌ๋ผ๋ ๋ฒจ
	book_id varchar2(100) PRIMARY KEY
	, std_id varchar2(100) REFERENCES student (id)
	, rent_date DATE
);
-- ์ปฌ๋ผ๋ช ์๋ฃํ(๊ธธ์ด) references ์ฐธ์กฐ๋์ํ์ด๋ธ๋ช (์ฐธ์กฐ๋์ ์ปฌ๋ผ๋ช)

INSERT INTO bookshelf VALUES ('501','003',sysdate);
SELECT * FROM bookshelf;

-- ์ฐธ์กฐ๋๊ณ  ์๋ ID -> 002๊ฐ ์๋ ํ์ ์ญ์ ํ๊ณ  ์ถ์ ๋
-- ์ธ๋ํค ์ฌ์ฉ : ์ฐธ์กฐ๋๊ณ  ์๋ ์ปฌ๋ผ์ ๋ฐ์ดํฐ๋ฅผ ๊ฐ์ง๊ณ  ์๋ ์์ ์ปฌ๋ผ์ด ์๋ค๋ฉด
-- ์๋ณธ ํ์ด๋ธ์ ๋ฐ์ดํฐ ์ญ์  X
SELECT * FROM student;
DELETE FROM student WHERE id = '003';


```

- ์ธ๋ํค ์ญ์ ์ต์
  - ๋ถ๋ชจํ์ด๋ธ์์ ๋ฐ์ดํฐ ์ญ์  ํ  ๋ ์์ ํ์ด๋ธ์ ์๋ ๋ฐ์ดํฐ๋ฅผ ์ด๋ค ๋ฐฉ์์ผ๋ก ์ฒ๋ฆฌํ ์ง ๊ฒฐ์ 
  - ์ ์ฝ์กฐ๊ฑด์ ๊ฑธ ๋ ์ญ์  ์ต์๋ ํจ๊ป ๊ฑธ์ด ์ค๋ค.
  - (๊ธฐ๋ณธ๊ฐ)์ผ๋ก ๋ถ๋ ์ต์์ on delete no action ์ด๋ค.
  - ์์ ์ ์ฐธ์กฐํ๋ ๋ฐ์ดํฐ๊ฐ ์๋ค๋ฉด ์ญ์ ํ  ์ ์๋ค.

`on delete set null;`

- ์ฐธ์กฐํ๊ณ  ์๋ ๋ถ๋ชจ ๋ฐ์ดํฐ๊ฐ ์ฌ๋ผ์ง๋ฉด ์์ ๋ฐ์ดํฐ๋ฅผ NULL๋ก ์ค์ 

```sql
CREATE TABLE bookshelf( -- ์ปฌ๋ผ๋ ๋ฒจ
	book_id varchar2(100) PRIMARY KEY
	, std_id varchar2(100) REFERENCES student (id) ON DELETE SET NULL
	, rent_date DATE
);
SELECT * FROM bookshelf;
DELETE FROM student WHERE id = '003';
```

`on delete cascade;`

- ์ฐธ์กฐํ๋ ๋ถ๋ชจ๋ฐ์ดํฐ๊ฐ ์ญ์ ๋๋ฉด ์ฐธ์กฐํ๋ ์์๋ฐ์ดํฐ๋ ํจ๊ป ์ญ์ ๋๋ค.
- ๊ฒ์๊ธ์ด ์ญ์ ๋๋ฉด ๋๊ธ๋ ์ญ์ ๋๋ค.

```sql
CREATE TABLE bookshelf( -- ์ปฌ๋ผ๋ ๋ฒจ
	book_id varchar2(100) PRIMARY KEY
	, std_id varchar2(100) REFERENCES student (id) ON DELETE cascade
	, rent_date DATE
);
SELECT * FROM bookshelf;
INSERT INTO bookshelf VALUES ('501','003',sysdate);

DELETE FROM student WHERE id = '003';

```

5. CHECK

- ํด๋น ์ปฌ๋ผ์ ์๋ ฅ๋๊ฑฐ๋ ์์ ๋์ด ๋ค์ด์ค๋ ๊ฐ์ ์ฒดํฌํด ์ค์ ํ ๊ฐ๋ง ๋ค์ด์ฌ ์ ์๊ฒ๋ ์ ํ

```sql
DROP TABLE user_cons;

CREATE TABLE user_cons(
	NO NUMBER
	, id varchar2(100)
	, pw varchar2(100)
	, gender varchar2(10) CHECK (gender IN ('๋จ','์ฌ'))
	, PRIMARY KEY (NO,id)
);
SELECT * FROM user_cons;
INSERT INTO user_cons VALUES (1,'ab123','asdfg','๋ง๊ณ ');
INSERT INTO user_cons VALUES (1,'ab123','asdfg','์ฌ');

DROP TABLE temp;
CREATE TABLE temp(
	date_one DATE
	, date_two DATE DEFAULT sysdate
);
INSERT INTO temp VALUES(sysdate, default); -- DEFAULT ํค์๋๋ก ๊ฐ ์ฝ์
SELECT * FROM temp;

```

---
emoji: 🪤
title: 데이터베이스 5일차 정리 - DB_DDL(데이터정의어), 제약조건(Constraints)
date: '2022-04-05 20:21:00'
author: bontaedev
tags: database oracle webdev study
categories: database
---

## DDL(Data Definition Language)

- 데이터 정의어

### drop : 테이블을 삭제하기 위해 사용하는 구문

DROP TABLE temp;

### ALTER

- 테이블에 정의된 내용을 수정하고자 할 때 사용하는 데이터 정의어
- 컬럼 추가삭제, 제약조건 추가삭제, 컬럼의 자료형 변경, DEFAULT 값 변경
- 테이블명,컬럼명,제약조건의 이름 변경

```sql
-- 이미 존재하는 테이블에 새로운 컬럼 추가
ALTER TABLE MEMBER ADD (name varchar2(100));

-- 새로운 컬럼 추가 (age) + default
ALTER TABLE MEMBER ADD (age MEMBER DEFAULT 0);

-- 제약조건 추가 - unique 추가
-- 추가할 제약조건의 이름도 지어줌
ALTER TABLE MEMBER ADD constraints id_unq unique(id);

SELECT constraint_name, constraint_type
FROM USER_CONSTRAINTS WHERE TABLE_name = 'MEMBER';

-- 제약조건 추가 - pw컬럼에 Not null 제약조건 추가
-- add로 접근할 수 없고 modify로
ALTER TABLE MEMBER ADD CONSTRAINT pw_nn NOT NULL(pw); -- x
ALTER TABLE MEMBER MODIFY pw CONSTRAINT pw_nn NOT NULL;

-- 컬럼명 수정 - pw 컬럼을 Password라고 변경
ALTER TABLE MEMBER RENAME COLUMN pw TO password;
DESC MEMBER;

-- 컬럼의 데이터 타입 수정 - name varchar2(100) -> char(100)
ALTER TABLE MEMBER MODIFY name char(100);

-- 컬럼의 삭제 (age 컬럼 삭제)
ALTER TABLE MEMBER DROP COLUMN age;

-- 제약조건 삭제 -- password 컬럼의 제약조건 삭제
-- 제약조건의 이름을 먼저 알야야 함
SELECT constraint_name  FROM USER_CONSTRAINTS WHERE table_name='MEMBER';
ALTER TABLE MEMBER DROP CONSTRAINT pw_nn;


-- 제약조건명 수정
ALTER TABLE MEMBER RENAME CONSTRAINT SYS_C007112 TO no_pk;

-- 테이블명 변경
ALTER TABLE MEMBER RENAME TO tb1_member;
```

## 제약조건(Constraints)

- 테이블을 생성할 때 구성하는 컬럼에 들어갈 데이터에 대해 제약조건을 설정하는 것
- 데이터의 일관성과 정확성을 유지하기 위해서 (데이터 무결성)
  <br>
- `NOT NULL` : 해당 컬럼에 null 값이 들어갈 수 없음.
- `UNIQUE` : 중복된 값을 허용하지 않음
- `Primary Key (기본키)` : (NOT NULL + Unique) 고유한 식별자로 사용하는 컬럼
- `Foreign Key (외래키)`: 두 테이블 간의 관계를 설정하고,
  - b테이블의 member_id 컬럼에 들어갈 수 있는 값이 A테이블의 ID에 있는 데이터여야 하는 경우
  - 예시 /게시글/댓글 의 관계
- `check` : 해당컬럼에 저장 가능한 값의 범위 조건을 지정해서 설정한 값만 허용

```sql
-- TYPE : P이면 primary key, C이면 Check or not null
SELECT CONSTRAINT_name, CONSTRAINT_type
FROM USER_CONSTRAINTS
	WHERE table_name = 'EMPLOYEE';
```

<br>

- 제약조건을 거는 위치 (컬럼레벨 / 테이블레벨)
  - 컬럼 레벨 : 컬럼명 자료형 옆에 제약조건을 명시하는 경우
  - 테이블 레벨 : 컬럼을 모두 정의한 후 마지막에 제약조건명 형식으로 제약조건을 걸어주는 방식
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

- Null 값을 허용X : 해당 컬럼에 반드시 값이 기록되어야 하는 경우

```sql
CREATE TABLE USER_nocons(
	no NUMBER
	, pw varchar2 (100)
	, name varchar2(100)
	, gender varchar2(10)
);
SELECT * FROM user_nocons;
INSERT INTO USER_nocons VALUES (1,'abc123','tom','남');
INSERT INTO USER_nocons VALUES (1,null,null,'여');

DROP TABLE user_cons;

CREATE TABLE user_cons(
-- 컬럼형 자료형(길이) 제약조건
	NO NUMBER unique
	, pw varchar2(100) NOT NULL
	, name varchar2(100) NOT NULL
	, gender varchar2(10)
);
SELECT * FROM USER_cons;
INSERT INTO user_cons VALUES (1,'aaa555','paul','남');
INSERT INTO user_cons VALUES (2,NULL,NULL,'여');
-- 데이터를 삽입할 때부터 제약조건에 부합하지 않는다면 데이터가 들어가지 않음
```

2. UNIQUE

- 해당 컬럼에 중복값을 제한하는 제약조건
- Null값도 들어감, 값을 안넣어도 됨

```sql
-- NO NUMBER unique
SELECT * FROM USER_nocons;
INSERT INTO user_nocons VALUES (1,'eee555','will','남');
INSERT INTO user_cons2 VALUES (1,'asdf','sam','남');
```

3. Primary Key (기본키)

- 컬럼의 데이터가 고유하고 null을 하용하지 않음 (고유 식별자)
- 하나의 테이블에서 하나만 걸어줄 수 있다. (고유식별자)
- unique + not null 제약조건은 하나의 테이블에서도 여러번 사용이 가능하기 때문에 식별자는 아니지만 중복값과 NULL을 체크할 때 사용

```sql
CREATE TABLE user_cons(
	NO NUMBER PRIMARY KEY
	, id varchar2(100) unique NOT NULL
	, pw varchar2(100) NOT NULL
	, nickname varchar2(200) UNIQUE NOT NULL
	, name varchar2(100) NOT NULL
	, gender varchar2(10)
);

INSERT INTO user_cons VALUES (1,'aaa555','paul','남');
INSERT INTO user_cons VALUES (2,'aaa555','paul','남');
```

- primary key에 대해 하나의 컬럼이 아닌 여러개의 컬럼에 대한 복합키 형태로 적용을 시키고 싶다면 컬럼레벨 에서는 불가
- 복합키 형태로 no,id 지정

```sql
CREATE TABLE user_cons(
	NO NUMBER
	, id varchar2(100)
	, pw varchar2(100)
	, gender varchar2(10)
	, PRIMARY KEY (NO,id)
);
```

4. Foreign Key (외래키) : 참조 무결성을 지키기 위해서

- 참조된 다른 테이블이 제공하는 값만 사용할 수 있도록 제약하고 싶을 때.
- 참조하는 컬럼과 참조되는 컬럼을 통해 두 테이블 간에 관계가 생성이 됨.
- 참조하는 컬럼이 참조되는 컬럼에 있는 값과 일치하거나, null 값만 가질 수 있음.
- 참조하는 컬럼 : 참조 대상을 참조하는 테이블의 컬럼 (B테이블)
- 참조되는 컬럼 : 참조 대상이 되는 테이블 컬럼 (A*학생*테이블)

```sql

-- 학생 테이블 / 대여 테이블
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

CREATE TABLE bookshelf( -- 테이블레벨
	book_id varchar2(100) PRIMARY KEY
	, std_id varchar2(100)
	, rent_date DATE
	, foreign KEY (std_id) REFERENCES student (id)
);

-- foreign key : (참조하는 컬럼) references 참조대상테이블 (참조대상컬럼)
CREATE TABLE bookshelf( -- 컬럼레벨
	book_id varchar2(100) PRIMARY KEY
	, std_id varchar2(100) REFERENCES student (id)
	, rent_date DATE
);
-- 컬럼명 자료형(길이) references 참조대상테이블명 (참조대상 컬럼명)

INSERT INTO bookshelf VALUES ('501','003',sysdate);
SELECT * FROM bookshelf;

-- 참조되고 있는 ID -> 002가 있는 행을 삭제하고 싶을 때
-- 외래키 사용 : 참조되고 있는 컬럼의 데이터를 가지고 있는 자식 컬럼이 있다면
-- 원본 테이블의 데이터 삭제 X
SELECT * FROM student;
DELETE FROM student WHERE id = '003';


```

- 외래키 삭제옵션
  - 부모테이블에서 데이터 삭제 할 때 자식 테이블에 있는 데이터를 어떤 방식으로 처리할지 결정
  - 제약조건을 걸 때 삭제 옵션도 함께 걸어 준다.
  - (기본값)으로 붙는 옵션은 on delete no action 이다.
  - 자신을 참조하는 데이터가 있다면 삭제할 수 없다.

`on delete set null;`

- 참조하고 있던 부모 데이터가 사라지면 자식 데이터를 NULL로 설정

```sql
CREATE TABLE bookshelf( -- 컬럼레벨
	book_id varchar2(100) PRIMARY KEY
	, std_id varchar2(100) REFERENCES student (id) ON DELETE SET NULL
	, rent_date DATE
);
SELECT * FROM bookshelf;
DELETE FROM student WHERE id = '003';
```

`on delete cascade;`

- 참조하는 부모데이터가 삭제되면 참조하는 자식데이터도 함께 삭제된다.
- 게시글이 삭제되면 댓글도 삭제된다.

```sql
CREATE TABLE bookshelf( -- 컬럼레벨
	book_id varchar2(100) PRIMARY KEY
	, std_id varchar2(100) REFERENCES student (id) ON DELETE cascade
	, rent_date DATE
);
SELECT * FROM bookshelf;
INSERT INTO bookshelf VALUES ('501','003',sysdate);

DELETE FROM student WHERE id = '003';

```

5. CHECK

- 해당 컬럼에 입력되거나 수정되어 들어오는 값을 체크해 설정한 값만 들어올 수 있게끔 제한

```sql
DROP TABLE user_cons;

CREATE TABLE user_cons(
	NO NUMBER
	, id varchar2(100)
	, pw varchar2(100)
	, gender varchar2(10) CHECK (gender IN ('남','여'))
	, PRIMARY KEY (NO,id)
);
SELECT * FROM user_cons;
INSERT INTO user_cons VALUES (1,'ab123','asdfg','망고');
INSERT INTO user_cons VALUES (1,'ab123','asdfg','여');

DROP TABLE temp;
CREATE TABLE temp(
	date_one DATE
	, date_two DATE DEFAULT sysdate
);
INSERT INTO temp VALUES(sysdate, default); -- DEFAULT 키워드로 값 삽입
SELECT * FROM temp;

```

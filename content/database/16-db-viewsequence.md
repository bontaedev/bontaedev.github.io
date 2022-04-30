---
emoji: 🪤
title: 데이터베이스 6일차 정리 - 뷰(View), 시퀀스(Sequence)
date: '2022-04-07 23:21:00'
author: bontaedev
tags: database oracle webdev study
categories: database
---

## 뷰 View

```sql
create view 뷰이름 as select ...
```

- 하나 이상의 테이블에서 원하는 데이터를 선택해서 새로운 가상테이블을 만들어 주는 것
- 뷰를 통해 만들어진 테이블이 물리적으로 존재하는 것은 아니고, 다른 테이블의 데이터만 조합해서 보여주는 것.
- 특정 계정이 원본 데이블에 접근해서 모든 데이터(불필요한 데이터)에 접근하는 걸 방지할 수 있음
- 뷰를 생성하는 권한 - 뷰의 내용을 수정하면 - 실제 원본 테이블의 데이터도 수정됨
- 원본 테이블의 내용이 수정되면 뷰의 내용도 수정된다. - 데이터 실시간 공유 (업데이트)

```sql
GRANT CREATE VIEW TO kh;

CREATE VIEW emp_view
AS SELECT emp_no, emp_name, email, phone
FROM EMPLOYEE;

SELECT * FROM emp_view;

UPDATE EMPLOYEE SET EMP_NAME ='김동일' WHERE emp_name = '선동일';

DROP VIEW emp_view;
COMMIT;
```

## 시퀀스(Sequence)

- 순차적으로 정수값을 자동을 생성하는 객체 (자동 번호 발생기)
- 옵션

  1. start with 숫자 : 몇번부터 번호를 시작할건지
  2. increment by 숫자 : 몇 단위로 숫자를 증가시킬건지
  3. maxvalue 숫자 / nomaxvalue : 시퀀스의 최대값 지정
  4. minvalue 숫자 / nominvalue : 시퀀스의 최소값 지정 / 지정x
  5. cycle / nocycle : 최대값에 도달하면 처음으로 돌아가 순번을 매길건지
  6. cache / nocache : 메모리상에 미리 시퀀스를 뽑아 올려두고 사용하는 것 / 메모리상에 올려놓지 X

- nextval : 현재값을 반환하고 시퀀스를 증가시킨다.
- currval : 현재값을 반환
- 접속후 nextval이 단 한번도 쓰이지 않았다면 사용할수 없음

```sql
CREATE SEQUENCE seq_temp
	START WITH 1
	INCREMENT BY 1
	NOMAXVALUE
	NOCYCLE
	nocache;

DROP sequence  seq_temp;

SELECT * FROM USER_SEQUENCES WHERE sequence_name = 'SEQ_TEMP';

SELECT seq_temp.nextval FROM dual;
SELECT seq_temp.currval FROM dual;

```

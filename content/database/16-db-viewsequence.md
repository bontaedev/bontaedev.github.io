---
emoji: πͺ€
title: λ°μ΄ν°λ² μ΄μ€ 6μΌμ°¨ μ λ¦¬ - λ·°(View), μνμ€(Sequence)
date: '2022-04-07 23:21:00'
author: bontaedev
tags: database oracle webdev study
categories: database
---

## λ·° View

```sql
create view λ·°μ΄λ¦ as select ...
```

- νλ μ΄μμ νμ΄λΈμμ μνλ λ°μ΄ν°λ₯Ό μ νν΄μ μλ‘μ΄ κ°μνμ΄λΈμ λ§λ€μ΄ μ£Όλ κ²
- λ·°λ₯Ό ν΅ν΄ λ§λ€μ΄μ§ νμ΄λΈμ΄ λ¬Όλ¦¬μ μΌλ‘ μ‘΄μ¬νλ κ²μ μλκ³ , λ€λ₯Έ νμ΄λΈμ λ°μ΄ν°λ§ μ‘°ν©ν΄μ λ³΄μ¬μ£Όλ κ².
- νΉμ  κ³μ μ΄ μλ³Έ λ°μ΄λΈμ μ κ·Όν΄μ λͺ¨λ  λ°μ΄ν°(λΆνμν λ°μ΄ν°)μ μ κ·Όνλ κ±Έ λ°©μ§ν  μ μμ
- λ·°λ₯Ό μμ±νλ κΆν - λ·°μ λ΄μ©μ μμ νλ©΄ - μ€μ  μλ³Έ νμ΄λΈμ λ°μ΄ν°λ μμ λ¨
- μλ³Έ νμ΄λΈμ λ΄μ©μ΄ μμ λλ©΄ λ·°μ λ΄μ©λ μμ λλ€. - λ°μ΄ν° μ€μκ° κ³΅μ  (μλ°μ΄νΈ)

```sql
GRANT CREATE VIEW TO kh;

CREATE VIEW emp_view
AS SELECT emp_no, emp_name, email, phone
FROM EMPLOYEE;

SELECT * FROM emp_view;

UPDATE EMPLOYEE SET EMP_NAME ='κΉλμΌ' WHERE emp_name = 'μ λμΌ';

DROP VIEW emp_view;
COMMIT;
```

## μνμ€(Sequence)

- μμ°¨μ μΌλ‘ μ μκ°μ μλμ μμ±νλ κ°μ²΄ (μλ λ²νΈ λ°μκΈ°)
- μ΅μ

  1. start with μ«μ : λͺλ²λΆν° λ²νΈλ₯Ό μμν κ±΄μ§
  2. increment by μ«μ : λͺ λ¨μλ‘ μ«μλ₯Ό μ¦κ°μν¬κ±΄μ§
  3. maxvalue μ«μ / nomaxvalue : μνμ€μ μ΅λκ° μ§μ 
  4. minvalue μ«μ / nominvalue : μνμ€μ μ΅μκ° μ§μ  / μ§μ x
  5. cycle / nocycle : μ΅λκ°μ λλ¬νλ©΄ μ²μμΌλ‘ λμκ° μλ²μ λ§€κΈΈκ±΄μ§
  6. cache / nocache : λ©λͺ¨λ¦¬μμ λ―Έλ¦¬ μνμ€λ₯Ό λ½μ μ¬λ €λκ³  μ¬μ©νλ κ² / λ©λͺ¨λ¦¬μμ μ¬λ €λμ§ X

- nextval : νμ¬κ°μ λ°ννκ³  μνμ€λ₯Ό μ¦κ°μν¨λ€.
- currval : νμ¬κ°μ λ°ν
- μ μν nextvalμ΄ λ¨ νλ²λ μ°μ΄μ§ μμλ€λ©΄ μ¬μ©ν μ μμ

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

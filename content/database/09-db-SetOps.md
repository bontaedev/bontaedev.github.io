---
emoji: ๐ชค
title: ๋ฐ์ดํฐ๋ฒ ์ด์ค 4์ผ์ฐจ ์ ๋ฆฌ - ์งํฉ์ฐ์ฐ์
date: '2022-04-04 20:21:00'
author: bontaedev
tags: database oracle webdev study
categories: database
---

## ์งํฉ ์ฐ์ฐ์ Set Operator

- ๋ ๊ฐ ์ด์์ ํ์ด๋ธ์ ์กฐ์ธ์์ด ์ฐ๊ด๋ ๋ฐ์ดํฐ๋ฅผ ์กฐํํ๋ ๋ฐฉ์
- ์ฌ๋ฌ ๊ฐ์ ์ง์๊ฒฐ๊ณผ(ResultSet)์ ์ฐ๊ฒฐํด์ ํ๋๋ก ๊ฒฐํฉํ๋ ๋ฐฉ์
- ๊ฐ ํ์ด๋ธ์์ ๋ฐํ๋ ๊ฒฐ๊ณผ๊ฐ์ ํ๋์ ํ์ด๋ธ๋ก ๊ฒฐํฉํ๋ ๋ฐฉ์
- ์ฌ๋ฌ๊ฐ์ sql๋ฌธ์ ์ฌ์ฉํด์ ํ๋์ ํ์ด๋ธ๋ก ๊ฒฐ๊ณผ๋ฅผ ๋ฐํ๋ฐ์์ผ ํ๋ ๊ฒฝ์ฐ

### UNION

- ํฉ์งํฉ. ์ค๋ณต๋ ๋ฐ์ดํฐ๋ฅผ ์ ๊ฑฐํ๊ณ  ์ฒซ๋ฒ์งธ ์ปฌ๋ผ์ ๊ธฐ์ค์ผ๋ก ์ค๋ฆ์ฐจ์ํ์ฌ ๋ฐ์ดํฐ๋ฅผ ๋ณด์ฌ์ค.
- ๊ฐ ํ์ด๋ธ์์ ์กฐํํ๋ ์ปฌ๋ผ ์๊ฐ ๋ค๋ฅด๋ฉด UNION ์ฌ์ฉX
- ์กฐํํ๋ ค๋ ์ปฌ๋ผ์ด ์๋ก ์ํธํธํ ๋ถ๊ฐํ ๋ฐ์ดํฐํ์์ด๋ฉด union ์ฌ์ฉ X (๋ฐ์ดํฐ์ ์ผ๊ด์ฑ ์ ์ง)

```sql
SELECT no_a FROM a;
SELECT no_b FROM b;

SELECT no_a FROM a
UNION
SELECT no_b FROM b;
```

### UNION ALL

- ํฉ์งํฉ. ์ค๋ณต๋ ๋ฐ์ดํฐ๋ฅผ ์ ๊ฑฐํ๊ณ  ์ ๋ ฌ์์ด ๋ฐ์ดํฐ๋ฅผ ๋ณด์ฌ์ค.
- ์กฐํํ ๊ฒฐ๊ณผ๊ฐ์ ์ฒซ๋ฒ์งธ ํ์ด๋ธ ์๋๋ก ๋๋ฒ์งธ ํ์ด๋ธ ๊ฒฐ๊ณผ๊ฐ์ ์ด์ด๋ถ์

```sql
SELECT no_a FROM A
UNION ALL
SELECT no_b FROM B;
```

### INTERSECT

- ๊ต์งํฉ. ๋ ํ์ด๋ธ์ ์ฟผ๋ฆฌ ๊ฒฐ๊ณผ์ค ๊ณตํต๋ ๊ฒฐ๊ณผ๊ฐ๋ง ๋ณด์ฌ์ค.

```sql
SELECT no_a FROM A
INTERSECT
SELECT no_b FROM B;
```

### MINUS

- ์ฐจ์งํฉ. ๋ ํ์ด๋ธ์ ์ฟผ๋ฆฌ ๊ฒฐ๊ณผ์ค ๊ณตํต๋ ์์๋ฅผ ๋บ ํ๋์ ํ์ด๋ธ๋ง ๋ณด์ฌ์ค

```sql
SELECT no_b FROM B
MINUS
SELECT no_a FROM A;
```

### ์์๋ฌธ์ 

```sql
SELECT
	emp_id, emp_name, dept_code, salary
FROM EMPLOYEE
	WHERE DEPT_CODE = 'D5';

SELECT
	emp_id, emp_name, dept_code, salary
FROM EMPLOYEE
	WHERE salary >= 3000000;

```

- employee ๋ถ์์ฝ๋๊ฐ D5์ธ ์ฌ๋์ ์ฌ๋ฒ, ์ฌ์๋ช, ๋ถ์์ฝ๋, ์๊ธ ์ถ๋ ฅ
- ์๊ธ์ด 300๋ง์ ์ด์์ธ ์ฌ์๋ค์ ์ฌ๋ฒ, ์ฌ์๋ช, ๋ถ์์ฝ๋, ์๊ธ ์ถ๋ ฅ
- ์ด ๋๊ฐ์ง ์ฟผ๋ฆฌ ๊ฒฐ๊ณผ๋ฅผ ์งํฉ ์ฐ์ฐ์๋ฅผ ์ด์ฉ

```sql
-- UNION ALL
SELECT
	emp_id, emp_name, dept_code, salary
FROM EMPLOYEE
	WHERE DEPT_CODE = 'D5'
UNION ALL
SELECT
	emp_id, emp_name, dept_code, salary
FROM EMPLOYEE
	WHERE salary >= 3000000;
-- INTERSECT
	SELECT
	emp_id, emp_name, dept_code, salary
FROM EMPLOYEE
	WHERE DEPT_CODE = 'D5'
INTERSECT
SELECT
	emp_id, emp_name, dept_code, salary
FROM EMPLOYEE
	WHERE salary >= 3000000;
-- MINUS
	SELECT
	emp_id, emp_name, dept_code, salary
FROM EMPLOYEE
	WHERE DEPT_CODE = 'D5'
MINUS
SELECT
	emp_id, emp_name, dept_code, salary
FROM EMPLOYEE
	WHERE salary >= 3000000;

```

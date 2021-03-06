---
emoji: ๐ชค
title: ๋ฐ์ดํฐ๋ฒ ์ด์ค 5์ผ์ฐจ ์ ๋ฆฌ - DB_TopN_๋ถ์(topNQuery)
date: '2022-04-05 21:02:03'
author: bontaedev
tags: database oracle webdev study
categories: database
---

## Top N ๋ถ์ (Top N Query)

- ์ปฌ๋ผ์์ ๊ฐ์ฅ ํฐ n๊ฐ์ ๊ฐ์ ํน์ ๊ฐ์ฅ ์์ n๊ฐ์ ๊ฐ์ ์์ฒญํ  ๋ ์ฌ์ฉ
- ์์/ํ์ n๊ฐ์ ๋ฐ์ดํฐ
- ํ์ฌ์์ ๊ฐ์ฅ ๋ง์ด ํ๋ฆฐ ์ ํ 10๊ฐ, ํ์ฌ์์ ๋ด๊ธ์ด ์ ์ผ ๋ง์ 10๊ฐ
- ๊ฒ์ํ ํ์ด์ง / ์กฐํ์๊ฐ ๋์ ์ธ๊ธฐ๊ธ

## ROWNUM

- ์ถ๋ ฅ๋๋ Select ๋ฌธ์ ํ๋ง๋ค ์๋์ ์ผ๋ก ์์๋ฅผ ๋งค๊ฒจ์ฃผ๋ ๊ฒ
- default๋ก ์๋ ์กด์ฌํ๋ ๋ฐ์ดํฐ์ ์์๋๋ก ์์๋ฅผ ๋งค๊ฒจ์ค๋ค.
- ์ฐ๋ฆฌ๊ฐ ์ํ๋ ๊ธฐ์ค์ ๋ง์ถฐ ์ด๋ฏธ ์ ๋ ฌ์ด ๋ ์ํ์ ๋ฐ์ดํฐ์ ๋ํด rownum -> ์์๋ฅผ ๋งค๊ฒจ์ผ ํจ
- ์ธ๋ผ์ธ ๋ทฐ(Inline View) : ์๋ธ์ฟผ๋ฆฌ ์์์ ์๊ธ์ด ์ ์ผ ํฐ ์์๋๋ก ์ผ๋จ ๋ฐ์ดํฐ๋ฅผ ์ ๋ ฌ
- ์ค์  ๋ฉ์ธ์ฟผ๋ฆฌ์์ rownum์ ์ฌ์ฉํ๊ฒ ๋๋ฉด ์ด๋ฏธ ์ ๋ ฌ๋ ๋ฐ์ดํฐ์ ๋ํด ์์๊ฐ ๋งค๊ฒจ์ง๊ฒ ๋๋ค.
- ์ธ๋ผ์ธ๋ทฐ๋ฅผ ๊ณ์ ์ฌ์ฉํ๋ฉด ์ฟผ๋ฆฌ๋ฌธ์ด ๊ธธ์ด์ง๋ค.

```sql
SELECT
	rownum, emp_name, salary
FROM (SELECT * FROM EMPLOYEE ORDER BY salary DESC);

-- ๊ฐ์ฅ ๋์ ๊ธ์ฌ๋ฅผ ๋ฐ๋ ํ ์ฌ๋์ ๋ํ ์์,emp_name,salary
SELECT
	rownum, emp_name, salary
FROM (SELECT * FROM EMPLOYEE ORDER BY salary desc)
	WHERE rownum = 1;

-- ๊ฐ์ฅ ๋์ ๊ธ์ฌ๋ฅผ ๋ฐ๋ 5๋ช์ ์์,emp_name,salary
SELECT
	rownum, emp_name, salary
FROM (SELECT * FROM EMPLOYEE ORDER BY salary desc)
	WHERE rownum <= 5;
```

### 1.ROW_NUMBER()

```sql
row_number() over(order by ์ปฌ๋ผ...)
SELECT
	ROW_NUMBER() OVER(ORDER BY SALARY desc) "์์"
	, emp_name
	, salary
FROM EMPLOYEE;
```

- over ์์ชฝ์ ์ปฌ๋ผ ์์์ ๋ฐ๋ผ ์ ๋ ฌํ ๋ค์ ์์๋ฅผ ๋งค๊ธด๋ค.
- ์ ๋ ฌ ๋ฐ์ดํฐ์ ์ค๋ณต๊ฐ์ด ์๋ค๋ฉด ์๋ ์์๋๋ก 19,20 ์ด๋ฐ ์์ผ๋ก ๋งค๊ฒจ์ค๋ค.
- ์์.
  - ์๊ธ์ ๊ฐ์ฅ ๋ง์ด ๋ฐ๋ top5
  - row_number ๋ก ์์ฑในํ ์์๋ ROWNUM์ผ๋ก ์ ๊ทผ ๊ฐ๋ฅ
  - rownum์ ์ฌ์ฉํ๊ฒ ๋๋ฉด ์๋ ๋ฐ์ดํฐ์ ์ ๋ ฌ ์์๋ฅผ ๊ธฐ์ค์ผ๋ก 5๊ฐ์ ๋ฐ์ดํฐ๊ฐ ๋ฝํ ๋์ค๊ณ 
  - ๊ทธ ๋ค์์ Select ๊ตฌ๋ฌธ์ row_number๋ฅผ ํตํด ์์๊ฐ ์ฌ์ ๋ ฌ ๋๋ ์ํฉ
  - where ์ ์ rownum์ ์ฌ์ฉํ  ์ ์๋ค.

### 2. RANK OVER

```sql
rank over(order by ์ปฌ๋ผ...)
SELECT
	RANK over(ORDER BY SALARY DESC) "์์"
	, emp_name
	, salary
FROM EMPLOYEE;
```

- over ์์ ์ปฌ๋ผ์ ๋ฐ๋ผ ์ ๋ ฌํ ๋ค์ ์์๋ฅผ ๋งค๊ธด๋ค.
- ์ค๋ณต๋๋ ๊ฒฝ์ฐ 19,19 ์ด๋ฐ์์ผ๋ก ๊ฐ์ ์์๋ฅผ ๋งค๊ธฐ๊ณ , ๊ฐ์ ์์๋ฅผ ๋งค๊ธด ๋ฐ์ดํฐ๋งํผ ๊ฑด๋๋ฐ์ด ๋ค์ ์์๋ฅผ ๋งค๊น.

### 3. DENSE_RANK()

```sql
SELECT
	DENSE_RANK() over(ORDER BY salary DESC) "์์"
	, emp_name
	, salary
FROM EMPLOYEE;
```

- over ์์ ์ปฌ๋ผ์ ๋ฐ๋ผ ์ ๋ ฌํ ๋ค์ ์์๋ฅผ ๋งค๊ธด๋ค.
- ์ค๋ณต๋๋ ๊ฒฝ์ฐ ๋๊ฐ์ ๋ฐฉ๋ฒ์ผ๋ก ์์๋ฅผ ๋งค๊ธฐ๊ณ , ๋ค์์๋ ์์ฐจ์ ์ผ๋ก ๋งค๊ธด๋ค. (19,19,20)
- ์ด ๋ฐ์ดํฐ์ ๊ฐ์์ ๋ ์์ ๋ฒํธ๊ฐ ์ผ์นํ์ง ์์ ์ ์์

## ์์ ๋ฌธ์ 

- ๊ธ์ฌ๋ฅผ ์ ์ผ ๋ง์ด ๋ฐ๋ 1~5์ ์ฌ์ด ์ฌ์ ์ ๋ณด
- ํ์ด๋ธ๋ช.\* : ๋ค๋ฅธ ๋ฐ์ดํฐ์ ํจ๊ป ๋ชจ๋  ์ ๋ณด๋ฅผ ์กฐํํ๊ณ  ์ถ์ ๋
- row_number ์ปฌ๋ผ์ ๋ณ์นญ์ผ๋ก ๊ฐ์ ธ์์ ์กฐํ

```sql
SELECT
	"์์"
	, emp_name
	, salary
FROM (SELECT
	ROW_NUMBER() over(ORDER BY salary DESC) "์์"
	, employee.*
	FROM EMPLOYEE);

SELECT *
FROM (SELECT
		ROW_NUMBER() over(ORDER BY salary desc) "์์"
		, emp_name "์ฌ์๋ช"
		, salary "๋ด๊ธ"
		FROM EMPLOYEE)
	WHERE "์์" <= 5;
```

- 5์์์ 10์ ์ฌ์ด์ ์ฌ์

```sql
SELECT *
FROM (SELECT
		ROW_NUMBER() over(ORDER BY salary desc) "์์"
		, emp_name "์ฌ์๋ช"
		, salary "๋ด๊ธ"
		FROM EMPLOYEE)
	WHERE "์์" BETWEEN 5 AND 10;
```

- ์ฐ๋ด(๋ณด๋์คํฌํจ-(salary + (salary*bonus)*12))์ด ๊ฐ์ฅ ๋์ ์์๋๋ก ์์ ๋งค๊น
- 10~15์ ์ฌ์ด์ธ ์ง์๋ค์ ์์, ์ฌ์๋ช, ์ฐ๋ด, ์ง๊ธ์ฝ๋, ๋ถ์์ฝ๋๊น์ง ์ถ๋ ฅ
- ๋ถ์์ฝ๋๊ฐ null์ด๋ผ๋ฉด ์ธํด

```sql
SELECT *
FROM (SELECT
		ROW_NUMBER() OVER(ORDER BY ((salary + (salary * NVL(bonus,0)))*12) DESC) "์์"
		, (salary + (salary * NVL(bonus,0))) "์๊ธ+๋ณด๋์ค"
		, emp_name "์ฌ์๋ช"
		, ((salary + (salary* NVL(bonus,0)))*12) "์ฐ๋ด"
		, job_code "์ง๊ธ์ฝ๋"
		, NVL(dept_code,'์์') "๋ถ์์ฝ๋"
	FROM EMPLOYEE)
	WHERE "์์" BETWEEN 10 AND 15;
```

- ๊ฐ์ฅ ๋ณด๋์ค๋ฅผ ๋ง์ด ๋ฐ๋ ์์ผ๋ก ์์๋ฅผ ๋งค๊น
- 4~8์์ธ ์ฌ์๋ค์ ์์, ์ด๋ฆ, ๊ธ์ฌ, ๋ณด๋์ค๋ฅผ ์ถ๋ ฅ
- ๋ฐ์ดํฐ์ null๊ฐ์ด ์๋ ์ํ์์ ์ ๋ ฌํ๋ฉด null ๊ฐ์ด ์ ์ผ ํฐ ๊ฐ์ผ๋ก ์ธ์ (์ ๋๋ก ์ ๋ ฌ ์๋จ)

```sql
-- rownum
SELECT *
FROM (SELECT
		row_number() OVER(ORDER BY (salary * NVL(bonus,0)) DESC) "์์"
		, emp_name "์ด๋ฆ"
		, salary "๊ธ์ฌ"
		, (salary * NVL(bonus,0)) "๋ณด๋์ค"
	FROM EMPLOYEE)
	WHERE "์์" BETWEEN 4 AND 8;

-- rank over
SELECT *
FROM (SELECT
		RANK() OVER(ORDER BY (NVL(bonus,0)) DESC) "์์"
		, emp_name "์ด๋ฆ"
		, salary "๊ธ์ฌ"
		, (NVL(bonus,0)) "๋ณด๋์ค"
	FROM EMPLOYEE)
	WHERE "์์" BETWEEN 4 AND 8;

-- dense_rank
SELECT *
FROM (SELECT
		DENSE_RANK() OVER(ORDER BY (NVL(bonus,0)) DESC) "์์"
		, emp_name "์ด๋ฆ"
		, salary "๊ธ์ฌ"
		, (NVL(bonus,0)) "๋ณด๋์ค"
	FROM EMPLOYEE)
	WHERE "์์" BETWEEN 4 AND 8;
```

```toc

```

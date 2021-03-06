---
emoji: ๐ชค
title: ๋ฐ์ดํฐ๋ฒ ์ด์ค 4์ผ์ฐจ ์ ๋ฆฌ - DB์๋ธ์ฟผ๋ฆฌ
date: '2022-04-04 23:21:00'
author: bontaedev
tags: database oracle webdev study
categories: featured database
---

## ์๋ธ์ฟผ๋ฆฌ (Sub Query)

- ํ๋์ SQL๋ฌธ ์์ ํฌํจ๋ ๋ค๋ฅธ SQL๋ฌธ
- ๋ฉ์ธ์ฟผ๋ฆฌ๊ฐ ์๋ธ์ฟผ๋ฆฌ๋ฅผ ํฌํจํ๋ ์ข์์  ๊ด๊ณ
- ์๋ธ์ฟผ๋ฆฌ๋ ์๊ดํธ๋ก ๋ฌถ์ด์ค / ์ฐ์ฐ์์ ์ค๋ฅธ์ชฝ์ ์์น / order by๋ subquey์์์ ์ฌ์ฉ๋ถ๊ฐ

```sql
SELECT * FROM EMPLOYEE;
-- ์ ์ง์ฐ ์ง์์ ๋งค๋์ ๋ช์ ์ถ๋ ฅ
-- ์ ์ง์ฐ ์ง์์ ๋งค๋์  ID

SELECT emp_name, manager_id
FROM EMPLOYEE
	WHERE EMP_NAME = '์ ์ง์ฐ'; -- 214

-- ๋งค๋์  ID์ ์ฌ๋ฒ์ด ๊ฐ์ ์ง์๋ช = ๋งค๋์ ๋ช
SELECT
	emp_id, emp_name
FROM EMPLOYEE
	WHERE EMP_ID = '214'; -- ๋ฐฉ๋ช์

SELECT
	emp_id, emp_name
FROM EMPLOYEE
	WHERE EMP_ID =
	(SELECT MANAGER_ID FROM EMPLOYEE WHERE EMP_NAME = '์ ์ง์ฐ');
```

## ์๋ธ์ฟผ๋ฆฌ ์ข๋ฅ

- ๋จ์ผํ, ๋ค์คํ, ๋ค์ค์ด, ๋ค์คํ๋ค์ค์ด, ์ํธ์ฐ๊ด, ์คํฌ๋ผ

### 1. ๋จ์ผํ ์๋ธ์ฟผ๋ฆฌ : ์๋ธ์ฟผ๋ฆฌ ์กฐํ๊ฒฐ๊ณผ ๊ฐ์ด 1๊ฐ ํ

```sql
-- ์  ์ง์์ ๊ธ์ฌํ๊ท ๋ณด๋ค ๊ธ์ฌ๋ฅผ ๋ง์ด ๋ฐ์ ์ฌ์์ ์ฌ๋ฒ, ์ฌ์๋ช, ์ง๊ธ์ฝ๋, ์๊ธ ์กฐํ
SELECT FLOOR(avg(salary)) FROM EMPLOYEE;
SELECT
	emp_id, emp_name, job_code, salary
FROM EMPLOYEE
	WHERE SALARY > 3047662;

-- ์๋ธ์ฟผ๋ฆฌ ์ฌ์ฉ
SELECT
	emp_id, emp_name, job_code, salary
FROM EMPLOYEE
	WHERE SALARY > (SELECT FLOOR(avg(salary)) FROM EMPLOYEE);

-- ์ค์ํด ์ง์๊ณผ ๊ธ์ฌ๊ฐ ๊ฐ์ ์ฌ์๋ค์ ๊ฒ์. ์ฌ๋ฒ,์ฌ์๋ช,๊ธ์ฌ ์ถ๋ ฅ (๋จ ์ค์ํ ์ถ๋ ฅ X)

SELECT salary FROM EMPLOYEE WHERE EMP_NAME = '์ค์ํด'; -- 2000000

SELECT
	emp_id, emp_name, salary
FROM EMPLOYEE
	WHERE SALARY = (SELECT salary FROM EMPLOYEE WHERE EMP_NAME = '์ค์ํด')
	AND EMP_NAME != '์ค์ํด';

-- employeeํ์ด๋ธ์์ ๊ธ์ฌ๊ฐ ์ ์ผ ๋์ ์ฌ๋๊ณผ ์ ์ผ ๋ฎ์ ์ฌ๋์ ์ฌ๋ฒ, ์ง์๋ช, ๊ธ์ฌ ์กฐํ

SELECT MAX(salary) FROM EMPLOYEE;

SELECT
	emp_id, emp_name, salary
FROM EMPLOYEE
	WHERE SALARY IN
	((SELECT MAX(salary) FROM EMPLOYEE),
	(SELECT MIN(salary) FROM EMPLOYEE));

-- D5๋ถ์ ์ง์๋ค์ ํ๊ท ์๊ธ(์์์ ๋ฒ๋ฆผ)๋ณด๋ค ๋ ๋ง์ ์๊ธ์ ๋ฐ๋ D1,D2๋ถ์ ์ง์์
-- ์ฌ๋ฒ, ๋ถ์๋ฒํธ, ์ฌ์๋ช, ์๊ธ ์กฐํ

SELECT FLOOR(AVG(salary)) FROM EMPLOYEE WHERE DEPT_CODE = 'D5';

SELECT
	emp_id, dept_code, emp_name, salary
FROM EMPLOYEE
	WHERE SALARY > (SELECT FLOOR(AVG(salary)) FROM EMPLOYEE WHERE DEPT_CODE = 'D5')
	AND DEPT_CODE IN ('D1','D2');
```

### 2. ๋ค์คํ ์๋ธ์ฟผ๋ฆฌ : ์กฐํ ๊ฒฐ๊ณผ๊ฐ ์ฌ๋ฌ๊ฐ(์ฌ๋ฌํ)

- ๋ค์คํ ์๋ธ์ฟผ๋ฆฌ ์์๋ != ์ฐ์ฐ์ ๋ชป์
- IN, NOT IN, ANY, ALL, EXISTS ๋ฑ๊ณผ ๊ฐ์ด ์ฐ์

```sql
-- ์ก์ข๊ธฐ ๋ฐ๋๋ผ ์ฌ์๊ณผ ์ํด์๋ ๋ถ์์ ๊ฐ์ ๋ถ์์๋ค์ ๋ชจ๋  ์ ๋ณด ์ถ๋ ฅ
SELECT emp_name, dept_code FROM EMPLOYEE WHERE EMP_NAME IN ('์ก์ข๊ธฐ','๋ฐ๋๋ผ');
SELECT * FROM EMPLOYEE WHERE DEPT_CODE IN ('D5','D9');

SELECT * FROM EMPLOYEE
	WHERE DEPT_CODE IN
	(SELECT DEPT_CODE FROM EMPLOYEE WHERE EMP_NAME IN ('์ก์ข๊ธฐ','๋ฐ๋๋ผ'));

-- ์ฐจํ์ฐ, ์ ์ง์ฐ ์ฌ์์ ๊ธ์ฌ๋ฑ๊ธ(sal_level)๊ณผ ๊ฐ์ ๋ฑ๊ธ์ ๊ฐ์ง
-- ์ฌ์์ ์ง๊ธ๋ช, ์ฌ์๋ช, ๊ธ์ฌ๋ฑ๊ธ ์ถ๋ ฅ

SELECT emp_name, sal_level FROM EMPLOYEE WHERE EMP_NAME IN ('์ฐจํ์ฐ','์ ์ง์ฐ');

SELECT
	JOB_NAME "์ง๊ธ๋ช"
	, emp_name "์ฌ์๋ช"
	, sal_level "๊ธ์ฌ๋ฑ๊ธ"
FROM EMPLOYEE JOIN JOB
	USING (job_code)
	WHERE SAL_LEVEL IN
	(SELECT SAL_LEVEL FROM EMPLOYEE WHERE EMP_NAME IN ('์ฐจํ์ฐ','์ ์ง์ฐ'));
```

```sql

-- IN
-- ์ง๊ธ์ด ๋ํ, ๋ถ์ฌ์ฅ์ด ์๋ ์ง์๋ค์ ์ฌ์๋ช, ๋ถ์๋ช, ์ง๊ธ์ฝ๋
-- ์ ๋ ฌ์ ๋ถ์๋ช, ์ฌ์๋ช ์์ผ๋ก ์ค๋ฆ์ฐจ์

SELECT * FROM EMPLOYEE;
SELECT * FROM DEPARTMENT;
SELECT * FROM job;

SELECT job_name, JOB_CODE FROM job WHERE JOB_NAME NOT IN ('๋ํ','๋ถ์ฌ์ฅ');

SELECT
	emp_name "์ฌ์๋ช"
	, dept_title "๋ถ์๋ช"
	, job_code "์ง๊ธ์ฝ๋"
	, job_name "์ง๊ธ๋ช"
FROM EMPLOYEE LEFT OUTER JOIN DEPARTMENT
	ON (dept_code = DEPT_ID)
	JOIN JOB USING (job_code)
	WHERE job_code IN
	(SELECT JOB_CODE FROM job WHERE job_name NOT IN ('๋ํ','๋ถ์ฌ์ฅ'))
	ORDER BY ๋ถ์๋ช, ์ฌ์๋ช;


-- ANY : ์๋ธ์ฟผ๋ฆฌ์ ๊ฒฐ๊ณผ ์ค์ ํ๋๋ผ๋ ์ฐธ์ด๋ผ๊ณ  ํ๋ค๋ฉด ์ฐธ
-- ๊ฐ > any(1,2,3) : ์ผ์ชฝ์ ์๋ ๊ฐ์ด ์ค๋ฅธ์ชฝ์ ์ต์๊ฐ๋ณด๋ค ํฌ๋ฉด ๋๋ค.
-- ๊ฐ < any(1,2,3) : ์ผ์ชฝ์ ์๋ ๊ฐ์ด ์ค๋ฅธ์ชฝ์ ์ต๋๊ฐ๋ณด๋ค ์์ผ๋ฉด ๋๋ค.
-- ๊ฐ = any(1,2,3) : IN๊ณผ ๊ฐ์ ์ญํ 
-- ๊ฐ != any(1,2,3) : NOT IN ๊ณผ ๊ฐ์ ์ญํ 

-- ๊ธ์ฌ๊ฐ 200๋ง์ ํน์ 300๋ง์๋ณด๋ค ํฐ ์ฌ๋์ ์ฌ์๋ช, ๊ธ์ฌ ์ถ๋ ฅ

SELECT emp_name , salary
FROM EMPLOYEE
WHERE SALARY > 2000000 OR SALARY > 3000000;

SELECT
	emp_name, salary
FROM EMPLOYEE
	WHERE SALARY < ANY (2000000,3000000);

SELECT
	emp_name, salary
FROM EMPLOYEE
	WHERE SALARY != ANY (2000000,3000000);

-- job_code๊ฐ J3์ธ ์ฌ์๋ค์ ๊ธ์ฌ๋ณด๋ค ๋ ๋ง์ ๊ธ์ฌ๋ฅผ ๋ฐ๋ ์ฌ์๋ค์ ์ด๋ฆ,๊ธ์ฌ

SELECT salary FROM EMPLOYEE WHERE JOB_CODE ='J3';

SELECT emp_name, salary
FROM EMPLOYEE
	WHERE SALARY > ANY
	(SELECT salary FROM EMPLOYEE WHERE JOB_CODE ='J3');

-- D1,D5 ๋ถ์์ฝ๋๋ฅผ ๊ฐ์ง ์ฌ์๋ค์ ๊ธ์ฌ๋ณด๋ค ์ ๊ฒ ๋ฐ๋ ์ฌ์๋ค์ ์ฌ์๋ช, ๊ธ์ฌ, ๋ถ์์ฝ๋ ์ถ๋ ฅ
-- ๋จ D1,D5 ๋ถ์ ์ง์์ ์ถ๋ ฅ X
-- ์ ๋ ฌ์ ๋ถ์์ฝ๋ ๊ธฐ์ค ์ค๋ฆ์ฐจ์ ์ถ๋ ฅ

SELECT salary FROM EMPLOYEE WHERE DEPT_CODE IN ('D1','D5');

SELECT
	emp_name "์ฌ์๋ช"
	, salary "๊ธ์ฌ"
	, dept_code "๋ถ์์ฝ๋"
FROM EMPLOYEE
	WHERE SALARY < ANY
	(SELECT salary FROM EMPLOYEE WHERE DEPT_CODE IN ('D1','D5'))
	AND NVL(DEPT_CODE,'์์') NOT IN ('D1','D5')
	ORDER BY ๋ถ์์ฝ๋;
-- NOT IN์ equal ๋น๊ต์ด๊ธฐ ๋๋ฌธ์ null์ IS NULL ๋น๊ต๋ก ํด์ผํ๋ค.



-- ALL : ์๋ธ์ฟผ๋ฆฌ ๊ฒฐ๊ณผ ์ค์ ๋ชจ๋  ๊ฒ์ด ์ฐธ์ด์ฌ์ผ ํ๋ค.
-- ๊ฐ > all (1,2,3) : ์ผ์ชฝ์ ๊ฐ์ด ๋ชจ๋  ๊ฐ๋ณด๋ค ์ปค์ผํ๋ค.
-- ๊ฐ < all (1,2,3) : ์ผ์ชฝ์ ๊ฐ์ด ๋ชจ๋  ๊ฐ๋ณด๋ค ์์์ผ ํ๋ค.

-- job_code๊ฐ J3์ธ ์ง์ ์ค์์ ๊ฐ์ฅ ํฐ ๊ธ์ฌ๋ณด๋ค ๋ ๋ง์ ๊ธ์ฌ๋ฅผ ๋ฐ๋ ์ฌ์๋ค์ ์ฌ์๋ช, ๊ธ์ฌ

SELECT salary FROM EMPLOYEE WHERE JOB_CODE = 'J3';

SELECT emp_name, salary
FROM EMPLOYEE
	WHERE salary < all(SELECT salary FROM EMPLOYEE WHERE JOB_CODE = 'J3');
```

### 3. ๋ค์ค์ด ์๋ธ์ฟผ๋ฆฌ : ์๋ธ์ฟผ๋ฆฌ ์กฐํ๊ฒฐ๊ณผ ๊ฐ์ด ์ฌ๋ฌ๊ฐ ์ด ์ผ๋

```sql
-- ํด์ฌํ ์ฌ์ง์ : ๊ฐ์๋ถ์, ๊ฐ์ ์ง๊ธ์ ํด๋นํ๋ ์ฌ์์ ์ฌ์๋ช, ์ง๊ธ์ฝ๋, ๋ถ์์ฝ๋, ์์ฌ์ผ ์กฐํ

SELECT dept_code, job_code
FROM EMPLOYEE
	WHERE ENT_YN = 'Y'
	AND SUBSTR(EMP_NO,8,1) = '2'; -- D8,J6

SELECT
	emp_name, job_code , dept_code, hire_date
FROM EMPLOYEE
	WHERE DEPT_CODE = 'D8' AND JOB_CODE = 'J6';

SELECT
	emp_name, job_code , dept_code, hire_date
FROM EMPLOYEE
	WHERE (DEPT_CODE, JOB_CODE) IN
	(SELECT dept_code, job_code FROM EMPLOYEE
	WHERE ENT_YN = 'Y' AND SUBSTR(EMP_NO,8,1) = '2');


-- ํ์ด์  ์ง์๊ณผ ๊ฐ์ Manager ๋ฅผ ๊ฐ์ง๊ณ  ์๊ณ , ๊ฐ์ ๊ธ์ฌ๋ ๋ฒจ์ ๊ฐ์ง๊ณ  ์๋ ์ฌ์์
-- ์ด๋ฆ, ๊ธ์ฌ๋ ๋ฒจ, ๋งค๋์  ID๋ฅผ ์กฐํ (ํ์ด์  ์ ์ธ)
SELECT * FROM EMPLOYEE;

SELECT manager_id, sal_level FROM EMPLOYEE WHERE emp_name = 'ํ์ด์ ';

SELECT
	emp_name, sal_level, manager_id
FROM EMPLOYEE
	WHERE (MANAGER_ID, SAL_LEVEL) IN
	(SELECT manager_id, sal_level FROM EMPLOYEE WHERE emp_name = 'ํ์ด์ ')
	AND EMP_NAME != 'ํ์ด์ ';

-- ๊ธฐ์ ์ง์๋ถ์ด๋ฉด์ ๊ธ์ฌ๊ฐ 200๋ง์์ธ ์ง์์
-- ์ฌ์๋ช, ๋ถ์์ฝ๋, ๊ธ์ฌ, ๋ถ์์ ์ง์ญ๋ช ์ถ๋ ฅ
SELECT * FROM DEPARTMENT;
SELECT * FROM LOCATION;
SELECT * FROM EMPLOYEE;

SELECT dept_title, salary
FROM EMPLOYEE JOIN DEPARTMENT
	ON (DEPT_CODE = dept_id)
	WHERE dept_title = '๊ธฐ์ ์ง์๋ถ' AND salary = 2000000;

SELECT
	emp_name "์ฌ์๋ช"
	, dept_code "๋ถ์์ฝ๋"
	, salary "๊ธ์ฌ"
	, local_name "๋ถ์์ง์ญ๋ช"
FROM EMPLOYEE JOIN DEPARTMENT
	ON (DEPT_CODE = dept_id)
	JOIN LOCATION
	ON (location_id = local_code)
	WHERE dept_title = '๊ธฐ์ ์ง์๋ถ'
	AND salary = 2000000;

-- employee ํ์ด๋ธ๊ณผ Location ํ์ด๋ธ๋ง joinํ๊ณ  ๋ค์ค์ด ์๋ธ์ฟผ๋ฆฌ๋ฅผ ์ฌ์ฉ
-- ์ํ๋ ๋ฐ์ดํฐ๋ง ๋ฝ์ ๋ค์ ๋น๊ต

SELECT
	emp_name "์ฌ์๋ช"
	, dept_code "๋ถ์์ฝ๋"
	, salary "๊ธ์ฌ"
	, local_name "๋ถ์์ง์ญ๋ช"
	, local_code
FROM EMPLOYEE, LOCATION -- ๊ธฐ์ ์ง์๋ถ - dept_id / location_id ๋ฅผ ์ฐพ๊ธฐ
	WHERE (DEPT_CODE, local_code) IN
	(SELECT dept_id, location_id FROM DEPARTMENT
	WHERE dept_title = '๊ธฐ์ ์ง์๋ถ')
	AND SALARY = 2000000;

-- ์์ผ์ด 8์8์ผ์ธ ์ฌ์๋ค๊ณผ ๊ฐ์ ๋ถ์์ฝ๋, ์ง๊ธ์ฝ๋๋ฅผ ๊ฐ์ง ์ฌ์๋ค์
-- ์ฌ์๋ช, ์์ผ('0808'), ๋ถ์์ฝ๋, ๋ถ์๋ช ์ถ๋ ฅ

SELECT dept_code, job_code
FROM EMPLOYEE JOIN job
	USING (job_code)
	WHERE emp_no LIKE '__0808%';
```

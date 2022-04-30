---
emoji: 🪤
title: 데이터베이스 4일차 정리 - DB서브쿼리
date: '2022-04-04 23:21:00'
author: bontaedev
tags: database oracle webdev study
categories: featured database
---

## 서브쿼리 (Sub Query)

- 하나의 SQL문 안에 포함된 다른 SQL문
- 메인쿼리가 서브쿼리를 포함하는 종속적 관계
- 서브쿼리는 소괄호로 묶어줌 / 연산자의 오른쪽에 위치 / order by는 subquey안에서 사용불가

```sql
SELECT * FROM EMPLOYEE;
-- 전지연 직원의 매니저명을 출력
-- 전지연 직원의 매니저 ID

SELECT emp_name, manager_id
FROM EMPLOYEE
	WHERE EMP_NAME = '전지연'; -- 214

-- 매니저 ID와 사번이 같은 직원명 = 매니저명
SELECT
	emp_id, emp_name
FROM EMPLOYEE
	WHERE EMP_ID = '214'; -- 방명수

SELECT
	emp_id, emp_name
FROM EMPLOYEE
	WHERE EMP_ID =
	(SELECT MANAGER_ID FROM EMPLOYEE WHERE EMP_NAME = '전지연');
```

## 서브쿼리 종류

- 단일행, 다중행, 다중열, 다중행다중열, 상호연관, 스킬라

### 1. 단일행 서브쿼리 : 서브쿼리 조회결과 값이 1개 행

```sql
-- 전 직원의 급여평균보다 급여를 많이 받은 사원의 사번, 사원명, 직급코드, 월급 조회
SELECT FLOOR(avg(salary)) FROM EMPLOYEE;
SELECT
	emp_id, emp_name, job_code, salary
FROM EMPLOYEE
	WHERE SALARY > 3047662;

-- 서브쿼리 사용
SELECT
	emp_id, emp_name, job_code, salary
FROM EMPLOYEE
	WHERE SALARY > (SELECT FLOOR(avg(salary)) FROM EMPLOYEE);

-- 윤은해 직원과 급여가 같은 사원들을 검색. 사번,사원명,급여 출력 (단 윤은혜 출력 X)

SELECT salary FROM EMPLOYEE WHERE EMP_NAME = '윤은해'; -- 2000000

SELECT
	emp_id, emp_name, salary
FROM EMPLOYEE
	WHERE SALARY = (SELECT salary FROM EMPLOYEE WHERE EMP_NAME = '윤은해')
	AND EMP_NAME != '윤은해';

-- employee테이블에서 급여가 제일 높은 사람과 제일 낮은 사람의 사번, 직원명, 급여 조회

SELECT MAX(salary) FROM EMPLOYEE;

SELECT
	emp_id, emp_name, salary
FROM EMPLOYEE
	WHERE SALARY IN
	((SELECT MAX(salary) FROM EMPLOYEE),
	(SELECT MIN(salary) FROM EMPLOYEE));

-- D5부서 직원들의 평균월급(소수점버림)보다 더 많은 월급을 받는 D1,D2부서 직원의
-- 사번, 부서번호, 사원명, 월급 조회

SELECT FLOOR(AVG(salary)) FROM EMPLOYEE WHERE DEPT_CODE = 'D5';

SELECT
	emp_id, dept_code, emp_name, salary
FROM EMPLOYEE
	WHERE SALARY > (SELECT FLOOR(AVG(salary)) FROM EMPLOYEE WHERE DEPT_CODE = 'D5')
	AND DEPT_CODE IN ('D1','D2');
```

### 2. 다중행 서브쿼리 : 조회 결과가 여러개(여러행)

- 다중행 서브쿼리 앞에는 != 연산자 못씀
- IN, NOT IN, ANY, ALL, EXISTS 등과 같이 쓰임

```sql
-- 송종기 박나라 사원과 속해있는 부서와 같은 부서원들의 모든 정보 출력
SELECT emp_name, dept_code FROM EMPLOYEE WHERE EMP_NAME IN ('송종기','박나라');
SELECT * FROM EMPLOYEE WHERE DEPT_CODE IN ('D5','D9');

SELECT * FROM EMPLOYEE
	WHERE DEPT_CODE IN
	(SELECT DEPT_CODE FROM EMPLOYEE WHERE EMP_NAME IN ('송종기','박나라'));

-- 차태연, 전지연 사원의 급여등급(sal_level)과 같은 등급을 가진
-- 사원의 직급명, 사원명, 급여등급 출력

SELECT emp_name, sal_level FROM EMPLOYEE WHERE EMP_NAME IN ('차태연','전지연');

SELECT
	JOB_NAME "직급명"
	, emp_name "사원명"
	, sal_level "급여등급"
FROM EMPLOYEE JOIN JOB
	USING (job_code)
	WHERE SAL_LEVEL IN
	(SELECT SAL_LEVEL FROM EMPLOYEE WHERE EMP_NAME IN ('차태연','전지연'));
```

```sql

-- IN
-- 직급이 대표, 부사장이 아닌 직원들의 사원명, 부서명, 직급코드
-- 정렬은 부서명, 사원명 순으로 오름차순

SELECT * FROM EMPLOYEE;
SELECT * FROM DEPARTMENT;
SELECT * FROM job;

SELECT job_name, JOB_CODE FROM job WHERE JOB_NAME NOT IN ('대표','부사장');

SELECT
	emp_name "사원명"
	, dept_title "부서명"
	, job_code "직급코드"
	, job_name "직급명"
FROM EMPLOYEE LEFT OUTER JOIN DEPARTMENT
	ON (dept_code = DEPT_ID)
	JOIN JOB USING (job_code)
	WHERE job_code IN
	(SELECT JOB_CODE FROM job WHERE job_name NOT IN ('대표','부사장'))
	ORDER BY 부서명, 사원명;


-- ANY : 서브쿼리의 결과 중에 하나라도 참이라고 한다면 참
-- 값 > any(1,2,3) : 왼쪽에 있는 값이 오른쪽의 최소값보다 크면 된다.
-- 값 < any(1,2,3) : 왼쪽에 있는 값이 오른쪽의 최대값보다 작으면 된다.
-- 값 = any(1,2,3) : IN과 같은 역할
-- 값 != any(1,2,3) : NOT IN 과 같은 역할

-- 급여가 200만원 혹은 300만원보다 큰 사람의 사원명, 급여 출력

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

-- job_code가 J3인 사원들의 급여보다 더 많은 급여를 받는 사원들의 이름,급여

SELECT salary FROM EMPLOYEE WHERE JOB_CODE ='J3';

SELECT emp_name, salary
FROM EMPLOYEE
	WHERE SALARY > ANY
	(SELECT salary FROM EMPLOYEE WHERE JOB_CODE ='J3');

-- D1,D5 부서코드를 가진 사원들의 급여보다 적게 받는 사원들의 사원명, 급여, 부서코드 출력
-- 단 D1,D5 부서 직원은 출력 X
-- 정렬은 부서코드 기준 오름차순 출력

SELECT salary FROM EMPLOYEE WHERE DEPT_CODE IN ('D1','D5');

SELECT
	emp_name "사원명"
	, salary "급여"
	, dept_code "부서코드"
FROM EMPLOYEE
	WHERE SALARY < ANY
	(SELECT salary FROM EMPLOYEE WHERE DEPT_CODE IN ('D1','D5'))
	AND NVL(DEPT_CODE,'없음') NOT IN ('D1','D5')
	ORDER BY 부서코드;
-- NOT IN은 equal 비교이기 때문에 null은 IS NULL 비교로 해야한다.



-- ALL : 서브쿼리 결과 중에 모든 것이 참이여야 한다.
-- 값 > all (1,2,3) : 왼쪽의 값이 모든 값보다 커야한다.
-- 값 < all (1,2,3) : 왼쪽의 값이 모든 값보다 작아야 한다.

-- job_code가 J3인 직원 중에서 가장 큰 급여보다 더 많은 급여를 받는 사원들의 사원명, 급여

SELECT salary FROM EMPLOYEE WHERE JOB_CODE = 'J3';

SELECT emp_name, salary
FROM EMPLOYEE
	WHERE salary < all(SELECT salary FROM EMPLOYEE WHERE JOB_CODE = 'J3');
```

### 3. 다중열 서브쿼리 : 서브쿼리 조회결과 값이 여러개 열 일때

```sql
-- 퇴사한 여직원 : 같은부서, 같은 직급에 해당하는 사원의 사원명, 직급코드, 부서코드, 입사일 조회

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


-- 하이유 직원과 같은 Manager 를 가지고 있고, 같은 급여레벨을 가지고 있는 사원의
-- 이름, 급여레벨, 매니저 ID를 조회 (하이유 제외)
SELECT * FROM EMPLOYEE;

SELECT manager_id, sal_level FROM EMPLOYEE WHERE emp_name = '하이유';

SELECT
	emp_name, sal_level, manager_id
FROM EMPLOYEE
	WHERE (MANAGER_ID, SAL_LEVEL) IN
	(SELECT manager_id, sal_level FROM EMPLOYEE WHERE emp_name = '하이유')
	AND EMP_NAME != '하이유';

-- 기술지원부이면서 급여가 200만원인 직원의
-- 사원명, 부서코드, 급여, 부서의 지역명 출력
SELECT * FROM DEPARTMENT;
SELECT * FROM LOCATION;
SELECT * FROM EMPLOYEE;

SELECT dept_title, salary
FROM EMPLOYEE JOIN DEPARTMENT
	ON (DEPT_CODE = dept_id)
	WHERE dept_title = '기술지원부' AND salary = 2000000;

SELECT
	emp_name "사원명"
	, dept_code "부서코드"
	, salary "급여"
	, local_name "부서지역명"
FROM EMPLOYEE JOIN DEPARTMENT
	ON (DEPT_CODE = dept_id)
	JOIN LOCATION
	ON (location_id = local_code)
	WHERE dept_title = '기술지원부'
	AND salary = 2000000;

-- employee 테이블과 Location 테이블만 join하고 다중열 서브쿼리를 사용
-- 원하는 데이터만 뽑은 다음 비교

SELECT
	emp_name "사원명"
	, dept_code "부서코드"
	, salary "급여"
	, local_name "부서지역명"
	, local_code
FROM EMPLOYEE, LOCATION -- 기술지원부 - dept_id / location_id 를 찾기
	WHERE (DEPT_CODE, local_code) IN
	(SELECT dept_id, location_id FROM DEPARTMENT
	WHERE dept_title = '기술지원부')
	AND SALARY = 2000000;

-- 생일이 8월8일인 사원들과 같은 부서코드, 직급코드를 가진 사원들의
-- 사원명, 생일('0808'), 부서코드, 부서명 출력

SELECT dept_code, job_code
FROM EMPLOYEE JOIN job
	USING (job_code)
	WHERE emp_no LIKE '__0808%';
```

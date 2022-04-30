---
emoji: 🪤
title: 데이터베이스 4일차 정리 - 집합연산자
date: '2022-04-04 20:21:00'
author: bontaedev
tags: database oracle webdev study
categories: database
---

## 집합 연산자 Set Operator

- 두 개 이상의 테이블을 조인없이 연관된 데이터를 조회하는 방식
- 여러 개의 질의결과(ResultSet)을 연결해서 하나로 결합하는 방식
- 각 테이블에서 반환된 결과값을 하나의 테이블로 결합하는 방식
- 여러개의 sql문을 사용해서 하나의 테이블로 결과를 반환받아야 하는 경우

### UNION

- 합집합. 중복된 데이터를 제거하고 첫번째 컬럼을 기준으로 오름차순하여 데이터를 보여줌.
- 각 테이블에서 조회하는 컬럼 수가 다르면 UNION 사용X
- 조회하려는 컬럼이 서로 상호호환 불가한 데이터타입이면 union 사용 X (데이터의 일관성 유지)

```sql
SELECT no_a FROM a;
SELECT no_b FROM b;

SELECT no_a FROM a
UNION
SELECT no_b FROM b;
```

### UNION ALL

- 합집합. 중복된 데이터를 제거하고 정렬없이 데이터를 보여줌.
- 조회한 결과값의 첫번째 테이블 아래로 두번째 테이블 결과값을 이어붙임

```sql
SELECT no_a FROM A
UNION ALL
SELECT no_b FROM B;
```

### INTERSECT

- 교집합. 두 테이블의 쿼리 결과중 공통된 결과값만 보여줌.

```sql
SELECT no_a FROM A
INTERSECT
SELECT no_b FROM B;
```

### MINUS

- 차집합. 두 테이블의 쿼리 결과중 공통된 요소를 뺀 하나의 테이블만 보여줌

```sql
SELECT no_b FROM B
MINUS
SELECT no_a FROM A;
```

### 예시문제

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

- employee 부서코드가 D5인 사람의 사번, 사원명, 부서코드, 월급 출력
- 월급이 300만원 이상인 사원들의 사번, 사원명, 부서코드, 월급 출력
- 이 두가지 쿼리 결과를 집합 연산자를 이용

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

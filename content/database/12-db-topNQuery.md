---
emoji: 🪤
title: 데이터베이스 5일차 정리 - DB_TopN_분석(topNQuery)
date: '2022-04-05 21:02:03'
author: bontaedev
tags: database oracle webdev study
categories: database
---

## Top N 분석 (Top N Query)

- 컬럼에서 가장 큰 n개의 값을 혹은 가장 작은 n개의 값을 요청할 때 사용
- 상위/하위 n개의 데이터
- 회사에서 가장 많이 팔린 제품 10개, 회사에서 봉급이 제일 많은 10개
- 게시판 페이징 / 조회수가 높은 인기글

## ROWNUM

- 출력되는 Select 문의 행마다 자동적으로 순위를 매겨주는 것
- default로 원래 존재하는 데이터의 순서대로 순위를 매겨준다.
- 우리가 원하는 기준에 맞춰 이미 정렬이 된 상태의 데이터에 대해 rownum -> 순서를 매겨야 함
- 인라인 뷰(Inline View) : 서브쿼리 안에서 월급이 제일 큰 순서대로 일단 데이터를 정렬
- 실제 메인쿼리에서 rownum을 사용하게 되면 이미 정렬된 데이터에 대해 순서가 매겨지게 된다.
- 인라인뷰를 계속 사용하면 쿼리문이 길어진다.

```sql
SELECT
	rownum, emp_name, salary
FROM (SELECT * FROM EMPLOYEE ORDER BY salary DESC);

-- 가장 높은 급여를 받는 한 사람에 대한 순위,emp_name,salary
SELECT
	rownum, emp_name, salary
FROM (SELECT * FROM EMPLOYEE ORDER BY salary desc)
	WHERE rownum = 1;

-- 가장 높은 급여를 받는 5명의 순위,emp_name,salary
SELECT
	rownum, emp_name, salary
FROM (SELECT * FROM EMPLOYEE ORDER BY salary desc)
	WHERE rownum <= 5;
```

### 1.ROW_NUMBER()

```sql
row_number() over(order by 컬럼...)
SELECT
	ROW_NUMBER() OVER(ORDER BY SALARY desc) "순위"
	, emp_name
	, salary
FROM EMPLOYEE;
```

- over 안쪽의 컬럼 순서에 따라 정렬한 다음 순위를 매긴다.
- 정렬 데이터에 중복값이 있다면 원래 순서대로 19,20 이런 식으로 매겨준다.
- 예시.
  - 월급을 가장 많이 받는 top5
  - row_number 로 생성ㄹ한 순위는 ROWNUM으로 접근 가능
  - rownum을 사용하게 되면 원래 데이터의 정렬 순서를 기준으로 5개의 데이터가 뽑혀 나오고
  - 그 다음에 Select 구문의 row_number를 통해 순서가 재정렬 되는 상황
  - where 절에 rownum을 사용할 수 없다.

### 2. RANK OVER

```sql
rank over(order by 컬럼...)
SELECT
	RANK over(ORDER BY SALARY DESC) "순위"
	, emp_name
	, salary
FROM EMPLOYEE;
```

- over 안의 컬럼에 따라 정렬한 다음 순위를 매긴다.
- 중복되는 경우 19,19 이런식으로 같은 순위를 매기고, 같은 순위를 매긴 데이터만큼 건너뛰어 다음 순위를 매김.

### 3. DENSE_RANK()

```sql
SELECT
	DENSE_RANK() over(ORDER BY salary DESC) "순위"
	, emp_name
	, salary
FROM EMPLOYEE;
```

- over 안의 컬럼에 따라 정렬한 다음 순위를 매긴다.
- 중복되는 경우 똑같은 방법으로 순위를 매기고, 다음에는 순차적으로 매긴다. (19,19,20)
- 총 데이터의 개수와 끝 순위 번호가 일치하지 않을 수 있음

## 예제문제

- 급여를 제일 많이 받는 1~5위 사이 사원 정보
- 테이블명.\* : 다른 데이터와 함께 모든 정보를 조회하고 싶을 때
- row_number 컬럼은 별칭으로 가져와서 조회

```sql
SELECT
	"순위"
	, emp_name
	, salary
FROM (SELECT
	ROW_NUMBER() over(ORDER BY salary DESC) "순위"
	, employee.*
	FROM EMPLOYEE);

SELECT *
FROM (SELECT
		ROW_NUMBER() over(ORDER BY salary desc) "순위"
		, emp_name "사원명"
		, salary "봉급"
		FROM EMPLOYEE)
	WHERE "순위" <= 5;
```

- 5위에서 10위 사이의 사원

```sql
SELECT *
FROM (SELECT
		ROW_NUMBER() over(ORDER BY salary desc) "순위"
		, emp_name "사원명"
		, salary "봉급"
		FROM EMPLOYEE)
	WHERE "순위" BETWEEN 5 AND 10;
```

- 연봉(보너스포함-(salary + (salary*bonus)*12))이 가장 높은 순서대로 순위 매김
- 10~15위 사이인 직원들의 순위, 사원명, 연봉, 직급코드, 부서코드까지 출력
- 부서코드가 null이라면 인턴

```sql
SELECT *
FROM (SELECT
		ROW_NUMBER() OVER(ORDER BY ((salary + (salary * NVL(bonus,0)))*12) DESC) "순위"
		, (salary + (salary * NVL(bonus,0))) "월급+보너스"
		, emp_name "사원명"
		, ((salary + (salary* NVL(bonus,0)))*12) "연봉"
		, job_code "직급코드"
		, NVL(dept_code,'없음') "부서코드"
	FROM EMPLOYEE)
	WHERE "순위" BETWEEN 10 AND 15;
```

- 가장 보너스를 많이 받는 순으로 순위를 매김
- 4~8위인 사원들의 순위, 이름, 급여, 보너스를 출력
- 데이터에 null값이 있는 상태에서 정렬하면 null 값이 제일 큰 값으로 인식 (제대로 정렬 안됨)

```sql
-- rownum
SELECT *
FROM (SELECT
		row_number() OVER(ORDER BY (salary * NVL(bonus,0)) DESC) "순위"
		, emp_name "이름"
		, salary "급여"
		, (salary * NVL(bonus,0)) "보너스"
	FROM EMPLOYEE)
	WHERE "순위" BETWEEN 4 AND 8;

-- rank over
SELECT *
FROM (SELECT
		RANK() OVER(ORDER BY (NVL(bonus,0)) DESC) "순위"
		, emp_name "이름"
		, salary "급여"
		, (NVL(bonus,0)) "보너스"
	FROM EMPLOYEE)
	WHERE "순위" BETWEEN 4 AND 8;

-- dense_rank
SELECT *
FROM (SELECT
		DENSE_RANK() OVER(ORDER BY (NVL(bonus,0)) DESC) "순위"
		, emp_name "이름"
		, salary "급여"
		, (NVL(bonus,0)) "보너스"
	FROM EMPLOYEE)
	WHERE "순위" BETWEEN 4 AND 8;
```

```toc

```

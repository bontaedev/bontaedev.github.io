---
emoji: πͺ€
title: λ°μ΄ν°λ² μ΄μ€ 6μΌμ°¨ μ λ¦¬ - DB νΈλμ­μ
date: '2022-04-06 23:02:42'
author: bontaedev
tags: database oracle webdev study
categories: database
---

## νΈλμ­μμ΄λ? Transaction

- νλ²μ μνλμ΄μΌνλ μμ λ¨μ
- νλμ μμμ μλ£νκΈ° μν΄μ κ°κ°μ νλ¦μ μ μμ μΌλ‘ μλ£λμλλ§ μμλ¨μλ₯Ό μ μμ μΌλ‘ μνλμλ€κ³  νλ¨νκ³  μλ£νλ κ³Όμ 

- νΈλμ­μ μμ

ex) ATM

- 1.  μΉ΄λμ½μ
- 2.  λ©λ΄ μ ν(μΈμΆ)
- 3.  κΈμ‘νμΈ / λΉλ°λ²νΈ μΈμ¦
- 4.  μ¬μ©μκ° μλ ₯ν κΈμ‘μ΄ λ½μ μ μλ κΈμ‘μΈμ§ νμΈ
- 5.  μ€μ  νκΈ λμ΄
- 6.  μΉ΄λ λ½κ³  λ

```sql
 == νκΈμ μΈμΆνλ€ μμ
 * -> 6λ²κΉμ§μ μμμ΄ μ μμ μΌλ‘ μλ£κ° λμ λ -> commit(μλ£ μμ )
 * -> 6λ²κΉμ§μ μμ μ€μ νλλΌλ λΉμ μ νλ¦μ΄ λ°μνλ©΄ κ·Έλλ λͺ¨λ  μμμ ROLLBACK(μ·¨μ)
 *
 * commit : νΈλμ­μ μμμ΄ μ μμ μΌλ‘ μλ£λλ©΄ λ³κ²½ λ΄μ©μ μκ΅¬μ μΌλ‘ μ μ₯ (λͺ¨λ  savepoint μ­μ )
 * savepoint <savepointλͺ> : νμ¬ νΈλμ­μ μμ μμ μλ€κ° μ΄λ¦ λΆμ¬ (νλμ νΈλ¦°μ­μ μμμ κ΅¬μ­μ λλλ κ²)
 *
 * rollback : νΈλμ­μ μμμ λͺ¨λ μ·¨μνκ³  μ΅κ·Όμ commit νλ μ§μ μ λμκ°λ κ².
 * rollback to savepointλͺ : ν΄λΉ savepointλ‘ λλμκ°λ€.
```

```sql
CREATE TABLE tbl_user (
	NO NUMBER UNIQUE
	, id varchar2(100) PRIMARY KEY
	, pw varchar2(100) NOT null
);

INSERT INTO tbl_user values(1,'user1','pw1');
INSERT INTO tbl_user values(2,'user2','pw2');
INSERT INTO tbl_user values(3,'user3','pw3');

SELECT * FROM tbl_user;

COMMIT;

INSERT INTO tbl_user values(4,'user4','pw4');

DELETE FROM tbl_user WHERE NO='4';

ROLLBACK;

INSERT INTO tbl_user values(5,'user5','pw5');
SAVEPOINT sp1;
INSERT INTO tbl_user values(6,'user6','pw6');
SELECT * FROM tbl_user;

rollback TO sp1;
```

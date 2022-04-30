---
emoji: 🪤
title: 데이터베이스 6일차 정리 - 데이터제어어(DCL)
date: '2022-04-06 20:21:00'
author: bontaedev
tags: database oracle webdev study
categories: database
---

## GRANT / REVOKE

- 사용자 또는 role(resource, connect, dba)에 대한 권한 부여
- system / 관리자 계정 접속 - 신규 사용자 생성 - grant 접속 권한 부여 - 리소스 권한 부여

```sql
CREATE USER test01 IDENTIFIED BY test01;
GRANT CONNECT, resource TO test01;

REVOKE SELECT, INSERT ON kh.coffee FROM test01;

-- system 계정에서 TEST01 계정한테 KH 계정이 가지고 있는 COFFEE테이블에 접근 권한 부여
GRANT SELECT ON kh.coffee TO test01;
GRANT INSERT ON kh.coffee TO test01;
INSERT INTO kh.coffee VALUES(...);
```

---
emoji: ðª¤
title: ë°ì´í°ë² ì´ì¤ 6ì¼ì°¨ ì ë¦¬ - ë°ì´í°ì ì´ì´(DCL)
date: '2022-04-06 20:21:00'
author: bontaedev
tags: database oracle webdev study
categories: database
---

## GRANT / REVOKE

- ì¬ì©ì ëë role(resource, connect, dba)ì ëí ê¶í ë¶ì¬
- system / ê´ë¦¬ì ê³ì  ì ì - ì ê· ì¬ì©ì ìì± - grant ì ì ê¶í ë¶ì¬ - ë¦¬ìì¤ ê¶í ë¶ì¬

```sql
CREATE USER test01 IDENTIFIED BY test01;
GRANT CONNECT, resource TO test01;

REVOKE SELECT, INSERT ON kh.coffee FROM test01;

-- system ê³ì ìì TEST01 ê³ì íí KH ê³ì ì´ ê°ì§ê³  ìë COFFEEíì´ë¸ì ì ê·¼ ê¶í ë¶ì¬
GRANT SELECT ON kh.coffee TO test01;
GRANT INSERT ON kh.coffee TO test01;
INSERT INTO kh.coffee VALUES(...);
```

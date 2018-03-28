---
layout: post
title:  "MySQL Check, Repair, Optimize"
date:   2018-02-07 11:47:00 +0900
tags:
- MySQL
- MariaDB
- Optimize
- Check
- Repair
---

# MySQL Check, Repair, Optimize

MySQL에서는 테이블이 손상 되었는지 여부를 확인(`check`)하고, 손상된 테이블일 경우에는 테이블을 복구(`repair`)하고, 테이블을 최적화(`optimize`) 하는 기능들을 제공한다.

테이블을 `optimize` 하다가 중간에 Abort 되어 테이블이 손상된 경우에 `repair` 명령어를 통해 복구할 수 있고, MyISAM 엔진의 테이블의 경우 row를 delete해도 index 데이터가 남아있으므로 테이블의 용량이 줄지 않는 경우가 있다.

이럴 경우에 테이블을 최적화(`optimize`)하는 것이 하나의 방법이다.

## MySQL 특정 테이블 손상 여부 확인(Check)

```sql
/* 체크할 Table이 속해있는 Database를 선택한다. */
mysql> use `Database명`;

/* Table의 손상 여부를 확인한다. */
mysql> CHECK TABLE `Table명`;

```


## MySQL 특정 테이블 복구(Repair)

```sql
/* 복구할 Table이 속해있는 Database를 선택한다. */
mysql> use `Database명`;

/* 손상된 테이블을 복구한다. */
mysql> REPAIR TABLE `Table명`;
```

## MySQL 특정 테이블 최적화(Optimize)

```sql
/* 최적화할 Table이 속해있는 Database를 선택한다. */
mysql> use `Database명`;

/* 테이블을 최적화한다. */
mysql> OPTIMIZE TABLE `Table명`;
```

## 특정 데이터베이스의 모든 테이블 확인/복구

```bash
# Shell에서 MySQL 홈 디렉토리의 바이너리 디렉토리로 접속한다.
$ cd [MYSQL_Home]/bin

# 해당 DB의 모든 테이블을 확인하고 복구한다.
$ ./mysqlcehck -u [DB User] -p[DB Password] --auto-repair [Database명]
```

## 특정 데이터베이스의 모든 테이블 최적화

```bash
# Shell에서 MySQL 홈 디렉토리의 바이너리 디렉토리로 접속한다.
$ cd [MYSQL_Home]/bin

# 해당 DB의 모든 테이블을 최적화한다.
$ ./mysqlcehck -u [DB User] -p[DB Password] --optimize [Database명]
```

## 자료 출처

- [Nota's story](http://nota.tistory.com/74)
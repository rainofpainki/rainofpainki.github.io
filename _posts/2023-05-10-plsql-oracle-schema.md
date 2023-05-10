---
layout: post
title: "Spring Boot schema.sql 에서 ORACLE PL/SQL 문법 사용하기 (ORA-06550 오류 해결방법)"
date: 2023-05-10 11:45:00 +0900
tags:
  - Spring Boot
  - Java
  - schema.sql
  - data.sql
  - PL/SQL
  - oracle
---

# 오류 내용

Oracle Database 에서는 IF EXISTS 미지원으로 인하여 PL/SQL 블록을 이용하여 아래와 같이 처리할 수 밖에 없다.

```sql
-- MY_TABLE 테이블 삭제
BEGIN
   EXECUTE IMMEDIATE 'DROP TABLE MY_TABLE';
EXCEPTION
   WHEN OTHERS THEN
      IF SQLCODE != -942 THEN
         RAISE;
      END IF;
END;
```

그러나 이렇게 할 경우 아래와 같은 오류가 발생한다.

```
nested exception is java.sql.SQLException: ORA-06550: 줄 1, 열48:PLS-00103: 심볼 "end-of-file"를 만났습니다 다음 중 하나가 기대될 때:
```

# 오류의 원인

Java 코드가 표시되지 않지만 schema.sql 실행시 ScriptUtil 의 메서드를 호출하게 되는데, 이 메서드에서 SQL 구분 기호 `;` 를 기본으로 사용하기 때문이다.

# 해결 방법

## 1. application.properties 에서 구분 기호 설정

- Spring Boot 2.5.0 이상

```
spring.sql.init.separator = ^^^ END OF SCRIPT ^^^
```

- Spring boot 2.5.0 미만

```
spring.datasource.separator = ^^^ END OF SCRIPT ^^^
```

## 2. schema.sql, data.sql 변경

### 변경 전

```sql
BEGIN
   EXECUTE IMMEDIATE 'DROP TABLE MY_TABLE';
EXCEPTION
   WHEN OTHERS THEN
      IF SQLCODE != -942 THEN
         RAISE;
      END IF;
END;

CREATE TABLE MY_TABLE (ID NUMBER NOT NULL, NAME VARCHAR2(50) NOT NULL);
```

### 변경 후

```sql
BEGIN
   EXECUTE IMMEDIATE 'DROP TABLE RESERVATION';
EXCEPTION
   WHEN OTHERS THEN
      IF SQLCODE != -942 THEN
         RAISE;
      END IF;
END;
^^^ END OF SCRIPT ^^^

CREATE TABLE MY_TABLE (ID NUMBER NOT NULL, NAME VARCHAR2(50) NOT NULL)^^^ END OF SCRIPT ^^^
```

위와 같이 변경한다. `^^^ END OF SCRIPT ^^^` 가 너무 길다면 `$`, `/` 등 다른 것으로 사용해도 된다.

# 참고

- https://github.com/spring-projects/spring-boot/wiki/Spring-Boot-2.5.0-Configuration-Changelog
- https://stackoverflow.com/questions/63171252/spring-boot-failed-to-run-oracle-plsql-script
- https://stackoverflow.com/questions/63171252/spring-boot-failed-to-run-oracle-plsql-script
- https://github.com/spring-projects/spring-framework/issues/19999
- https://stackoverflow.com/questions/38884306/unable-to-use-drop-table-if-exists-in-schema-sql-for-a-spring-boot-application/45097894#45097894

---
layout: post
title:  "MySQL Time Event Schedule"
date:   2018-02-08 10:07:00 +0900
categories: MySQL MariaDB Event TimeEvent Schedule
---

# MySQL EVENT JOB 설정하기

MySQL 5.1.7 에서부터는 crontab+shell 을 사용하지 않고 시간별로 EVENT JOB을 설정할 수 있다.


## Event Scheduler ON
MySQL 전역변수에서 event_scheduler를 ON 해준다.

```sql
SET GLOBAL event_scheduler = ON;
SET @@global.event_scheduler = ON;
/* 또는 */
SET GLOBAL event_scheduler = 1;
SET @@global.event_scheduler = 1;
```

## EVENT 기본 SQL 문

다음은 EVENT를 작성하는 기본 SQL문이다.

```sql
/* SQL */
CREATE EVENT [IF NOT EXISTS] 이벤트명
ON SCHEDULE 스케줄
[ON COMPLETION [NOT] PRESERVE]
[ENABLE | DISABLE]
[COMMENT '주석']
DO [BEGIN] 실행할 sql문; [실행할 sql문]; [END]
```

## 세부 설정

INTERVAL 구문을 통해 반복 주기를 지정할 수 있고, EVERY 를 통해 매일, 매분, 매시 등의 반복 지정도 가능하다.

STARTS 와 ENDS를 통해 반복의 시작일시, 종료일시의 지정도 가능하다.
```sql
/* 스케줄 */
{ AT 타임 [+ INTERVAL 간격 [+INTERVAL 간격...]]
| EVERY 간격 [STARTS 타임] [ENDS 타임] }
```

```sql
/* 타임 */
{CURRENT_TIMESTAMP | 년월일시의 리터럴}
```

```sql
/* 간격 */
{YEAR|QUARTER|MONTH|DAY|HOUR|MINUTE|WEEK|SECOND|YEAR_MONTH|DAY_HOUR|DAY_MINUTE|DAY_SECOND|HOUR_MINUTE|HOUR_SECOND|MINUTE_SECOND}
```

- ON SCHEDULE 구문을 쓰게되면 이벤트의 실행시간과 간격을 필수로 지정하고, DO 구문 뒤에 실행할 SQL문을 적으면 된다.

- 일회성으로 한번만 지정하는 경우에는 ON SCHEDULE AT {timestamp} 와 같은 식으로 지정이 가능하다. 예를 들면 ON SCHEDULE AT '2018-02-08 13:00:00' 과 같은 식으로 가능하다. 하지만 반드시 미래의 시간을 지정하여야 한다.

- +INTERVAL은 복수 지정도 가능하다. + INTERVAL 1 WEEK, + INTERVAL 4 HOUR 와 같이 지정할 수 있다.


- DO 아래에 지정하는 SQL문이 하나인 경우에는 BEGIN, END, DELIMITER 지정은 필요없다.

- 복수로 지정하는 경우에만 BEGIN ~END로 Stored Procedure 처럼 감싼다.
그 이유는 BEGIN ~END 안에 있는 SQL문은 세미콜론(;)으로 구분하므로 CREATE EVENT의 끝을 의미하는 세미콜론(;)하고 구분이 불가능하기 때문.

- ON COMPLETION PRESERVE는 이벤트가 완료하더라고 이벤트의 내용을 유지한채 두게 된다.


## 예제 SQL 

예제문은 아래와 같다.

```sql
CREATE EVENT IF NOT EXISTS evt_sessionClean
ON SCHEDULE 
	EVERY 3 DAY_HOUR
	COMMENT 'Clean up session at 03:00 daily'
	DO
		DELETE FROM admin.user_session;
```

위의 코드는 매일 03시에 admin DATABASE의 user_session 테이블의 모든 Row를 DELETE한다.

더 자세한 출처는 [공식문서](https://dev.mysql.com/doc/refman/5.7/en/create-event.html)나 [출처](http://linuxism.tistory.com/854)를 참고하도록 하자.


## 출처

1) https://dev.mysql.com/doc/refman/5.7/en/create-event.html
2) http://linuxism.tistory.com/854
3) http://h391106.tistory.com/257

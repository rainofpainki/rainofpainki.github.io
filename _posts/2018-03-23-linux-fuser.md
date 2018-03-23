---
layout: post
title:  "Linux fuser command"
date:   2018-02-23 13:27:00 +0900
categories: Linux CentOS Ubuntu fuser
---

# 리눅스에서 fuser 명령어 사용하기

fuser 명령어는 특정 파일을 삭제하거나 특정 파일의 사용자, 특정 파일을 사용하는 프로세스를 알고자 할 때 사용한다.

지정된 파일이 사용되고 있는 프로세스 ID를 확인하는 명령어로 지정된 파일과 PID를 KILL 또는 재시작할 수도 있다.

## 옵션

- \-a : 사용되고 있지 않은 파일까지도 표시한다.
- \-k : 지정된 파일과 관련된 모든 프로세스들을 KILL 한다.
- \-i : 프로세스를 KILL 하기전에 사용자에게 확인한다.
- \-n space : 지정된 공간(file, udp, or , tcp)내에서 검색한다.
- \-s : 결과를 간략히 출력한다.
- \-u : 프로세스 ID(PID)의 소유자를 보여준다.


## 사용법

1) 특정 파일이나 디렉토리를 사용하는 프로세스의 PID/사용자 를 확인할 때

```sh
# fuser -u /usr/bin/php7.0

/usr/bin/php7.0:      5723e(user1)  6627e(user2) 21109e(user3)
```

2) 특정 파일이나 디렉토리를 사용하는 프로세스를 모두 죽일 때

```sh
# fuser -k /usr/bin/php7.0

# php7.0을 사용하는 모든 프로세스를 죽인다.
```

3) 특정 파일이나 디렉토리를 사용하는 프로세스의 user/pid/접근 권한 등을 자세히 볼 때

```sh
# fuser -v /usr/bin/php7.0

                     USER        PID ACCESS COMMAND
/usr/bin/php7.0:     lunchbus   5723 ...e. php7.0
                     lunchbus   6627 ...e. php7.0
                     lunchbus  21109 ...e. php7.0
```


### ACCESS 항목의 의미

- \-c : 현재 디렉토리를 의미함.
- \-e : 실행 가능함을 표시함.
- \-f : 열려진 파일을 의미함.(default 이므로 생략됨)
- \-r : root 디렉토리를 의미함.
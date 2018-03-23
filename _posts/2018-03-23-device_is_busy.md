---
layout: post
title:  "umount: device is busy"
date:   2018-02-23 13:47:00 +0900
categories: Linux CentOS Ubuntu umount device_is_busy
---

# umount 할 때 device is busy 경고가 뜰 경우

mount된 디렉토리를 umount 를 할 시, 특정 프로세스&사용자가 해당 디렉토리를 사용하고 있다면 "device is busy" 메세지가 발생하며 umount가 되지 않는다.

```sh
$ umount /home/user1/data
umount: device is busy

# 강제로 실행해볼까? 
$ umount -f /home/user1/data
umount: device is busy
```

강제로 실행해도 결과는 똑같다.

## 디렉토리를 사용하는 프로세스를 강제로 죽이는 방법

```sh
$ fuser -ck /home/user1/data
# umount /home/user1/data
```

위 명령을 이용하면 프로세스를 kill하고 umount를 성공한다. 

## fuser 명령어에 대한 사용법

[링크](https://rainofpainki.github.io/linux-fuser/)를 참고하자.


### 출처

- [호스트웨이 서버운영가이드](http://faq.hostway.co.kr/Linux_ETC/1559)
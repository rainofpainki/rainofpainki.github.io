---
layout: post
title:  "How to install Zabbix agent for CentOS6"
date:   2018-02-01 14:57:00 +0900
categories: Linux Zabbix Zabbix-Server Zabbix-Agent Centos
---
# 자빅스(Zabbix) 설치 for CentOS6

회사에 CentOS6 서버에 Zabbix agent를 설치할 일이 발생하여 해당 포스트를 작성한다.

## 1. yum 저장소 update 및 Repository 추가

```sh
sudo su
yum update
rpm -ivh http://repo.zabbix.com/zabbix/3.4/rhel/6/x86_64/zabbix-release-3.4-1.el6.noarch.rpm
```

## 2. zabbix agent yum install

```sh
yum list zabbix*
yum install zabbix-agent
```


## 3. zabbix-agent 시작

```sh
service zabbix-agent start

# 부팅시에 실행 설정
chkconfig --level 345 zabbix-agent on
```

## 4. 포트 확인

```sh
netstat -tnlp | grep zabbix
```

## 5. Agent 파일 설정

```sh
vi /etc/zabbix/zabbix_agentd.conf
```

```
Server=Zabbix Server IP
ServerActive=Zabbix Server IP:10051
Hostname=Zabbix Agent IP
DebugLevel=4
```

## 6. 수집 확인

```sh
systemctl restart zabbix-agent
tail -f /var/log/zabbix/zabbix_agentd.log
```

SUCCEED를 확인 헀다면, zabbix_agentd의 DebugLevel을 다시 주석 처리한다.

당신의 방화벽에서 Zabbix Server에서 Agent로의 10051 포트 Inbound 정책을 허용하고, Zabbix Agent에서 Zabbix Server로의 10050 포트 Inbound 정책을 허용한다.

Zabbix Server 의 관리툴에 로그인하여 설정 -> 호스트 탭에서 해당 Agent를 추가할 수 있다.
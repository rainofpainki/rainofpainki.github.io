---
layout: post
title:  "How to install Selenium+PhantomJS"
date:   2018-01-30 15:52:00 +0900
categories: Python3 Selenium PhantomJS Docker
---
# Python3 Selenium + PhantomJS 설치

## 1. 가상 환경 구축

## 1.1. Docker를 통한 가상환경 구축

```sh
# Docker에 Ubuntu 이미지 가져오기
docker pull ubuntu:16.04
# Ubuntu를 실행하고 쉘에 들어가기
docker run -it ubuntu:16.04
```

위의 명령어로 Ubuntu 쉘에 로그인되면 Python3, Selenium을 설치한다.

### 1.1.1. Python3 설치

```sh
# 저장소 Update
apt-get update
# Python3, pip3 설치
apt-get install -y python3 python3-pip
```

> 이하에서 sudo 권한으로 apt를 설치하는 커맨드에서 sudo 를 제외해도 무관하다. root 권한으로 로그인하여 apt 설치해도 무방하나 root는 무한대의 권한을 가지고 있기 때문에 대부분의 시스템에서 불가능하도록 설정하는 것이 좋다. [참고](http://deois.tistory.com/42)

## 1.2. venv를 통한 패키지 가상환경 구축 

Docker 를 사용하지 않고 venv를 통하여 패키지 가상환경을 구축하고자 하는 경우에는 아래와 같이 진행한다.

### 1.2.1. Python3 설치

> docker와 같은 가상환경이 아니므로 sudo 를 이용해서 install 한다.

```sh
# 저장소 Update
sudo apt update
# Python3, pip3 설치
sudo apt install -y python3 python3-pip
# Python3 venv 설치
sudo apt install python3-venv
```

### 1.2.2. Python3 venv 생성

```sh
# 원하는 폴더로 이동 후
python3 -m venv venv(가상환경 이름)
```

### 1.2.3. Python3 venv 활성화

```sh
. venv/bin/activate
```

## 2.1. Selenium 및 크롤링 패키지 설치

### 2.2. pip update

```sh
pip3 install --upgrade pip
```

### 2.3. pip 리스트 체크

```sh
pip3 freeze
```

### 2.4. Request 설치

```sh
pip3 install requests
```

### 2.5. BeautifulSoup4 설치

```sh
pip3 install beautifulsoup4
```

### 2.6. Selenium 설치

```sh
pip3 install selenium
```

### 2.7. Scrapy 설치

> 크롤링 프레임워크인 Scrapy를 사용하고자 하는 경우에 설치한다.

```sh
# 의존성 패키지 설치 (Docker 환경이면 sudo를 제외한다)
sudo apt install libxml2-dev libxslt1-dev zlib1g-dev libffi-dev libssl-dev python3-dev gcc

# 패키지 설치
pip3 install scrapy
```

### 3. PhantomJS 설치

```sh
# 의존성 라이브러리 설치
sudo apt install libfontconfig1 fonts-migmix

# 바이너리 파일 다운로드 및 압축 해제
wget https://bitbucket.org/ariya/phantomjs/downloads/phantomjs-2.1.1-linux-x86_64.tar.bz2
tar xvf phantomjs-2.1.1-linux-x86_64.tar.bz2

# 바이너리 파일 위치 이동
sudo cp phantomjs-2.1.1-linux-x86_64/bin/phantomjs /usr/local/bin

# 스크린샷, 한글 입출력을 위한 한글 폰트 설치
sudo apt install fbterm fonts-nanum-coding
```


Docker를 이용한 경우에는 지금까지 저장한 사항을 Docker에 ubuntu-phantomjs 라는 이름으로 저장하고, exit로 Docker 쉘에서 빠져나온다. 컨테이너 ID를 확인한 뒤에 커밋한다.

```sh
docker ps -a
<컨테이너 ID>
docker commit <컨테이너 ID> ubuntu-phantomjs
```

이미지가 생성되면 다음 명령어를 실행해 컨테이너를 실행한다.

> 환경변수의 LANG에 UTF-8이 설정되어 있어야 한다.

```sh
docker run -i -t -v $HOME:$HOME \
-e ko_KR.UTF-8 \
-e PYTHONIOENCODING=utf_8 \
ubuntu-phantomjs /bin/bash
```

# 3. 자료 출처

- [프로그래머 미찐 티스토리 블로그](http://mizzhinp.tistory.com/entry/%EC%9A%B0%EB%B6%84%ED%88%AC-%EC%BD%98%EC%86%94%EC%97%90%EC%84%9C-%ED%95%9C%EA%B8%80-%EB%B3%B4%EA%B8%B0-%EA%B9%A8%EC%A7%90%ED%98%84%EC%83%81)
- [「파이썬을 이용한 머신러닝, 딥러닝 실전개발 입문」 위키북스 도서](http://wikibook.co.kr/python-machine-learning/)
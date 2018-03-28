---
layout: post
title:  "How to install Django in Windows"
date:   2018-03-28 13:27:00 +0900
categories: Django Python Windows
---

# 윈도우 환경에 파이썬, Django 설치하기

> 이 예제는 Windows 10, Git bash 기반으로 하였습니다.

## 1. 파이썬 설치하기

[https://www.python.org/downloads/](https://www.python.org/downloads/) 로 이동하여 Python 3.x.x 를 다운로드한다.

Python 3 버전을 설치하도록 한다.

 - 설치할 시 `Add python.exe to Path` 옵션이 있다면 `Will be installed on local hard drive`로 변경한다.
 
설치가 완료되면 명령 프롬프트나 git bash를 이용하여 python 이라고 입력하면 python 콘솔이 실행되는 것을 확인한다.
 
 
Python이 정상적으로 실행되는 것을 확인한 후, `Ctrl+C` 키를 눌러 파이썬을 종료한 후 명령 프롬프트에서 다음을 입력하고 `Enter`를 누른다.

```sh
$ python -m pip install -U pip
```  
 
위의 버전으로 pip (파이썬 패키지 관리자)를 설치한다.


## 2. 파이썬 가상 환경 설치하기

가상환경을 지원하지 않는 IDE를 사용한다면 가상 환경을 설치하여 소프트웨어가 의존하는 종속성을 해결한다.

> pip 등 패키지 관리자에서 사용되는 컴포넌트들이 프로젝트별로 분리시키는 환경으로서 다른 소프트웨어에 영향을 미치지 않고 프로젝트에 대한 작업을 할 수 있다. 


```sh
$ pip install virtualenv
```

virtualenv 가 설치되면 다음을 입력해서 가상 환경(프로젝트)을 만든다.

```sh
$ virtualenv flower-learning
```

> 이 예제에서는 프로젝트명을 `flower-learning` 이라고 한다.

디렉토리를 열면 다음과 같이 나타난다.

```sh
$ cd flower-learning
$ ls
Include/  Lib/  pip-selfcheck.json  Scripts/  tcl/
```

아래와 같이 실행하면 가상환경이 실행된다.

```sh
$ . Scripts/activate
```

가상환경이 실행되면 명령 프롬프트 위에 (프로젝트명) 이 생긴다. 가상환경의 실행은 터미널을 킬 때마다 해줘야 한다.

## 3. 장고 설치하기

파이썬과 가상환경을 모두 설치하였으므로 이제 장고 프레임워크를 설치한다.

```sh
$ pip install django==1.8.13
Collecting django==1.8.13
  Downloading Django-1.8.13-py2.py3-none-any.whl (6.2MB)
Installing collected packages: django
Successfully installed django-1.8.13
```

이 예제 에서는 장고 1.8.13 버전을 설치한다.


아래와 같이 장고 설치가 제대로 되었는지 확인한다.

```sh
$ winpty python.exe
Python 3.6.2 (v3.6.2:5fd33b5, Jul  8 2017, 04:57:36) [MSC v.1900 64 bit (AMD64)]
 on win32
Type "help", "copyright", "credits" or "license" for more information.
>>> import django
>>> django.get_version()
'1.8.13'
>>> quit()
```


> 필자와 같이 Git Bash를 사용하면 `python` 이라는 명령어로 실행했을 경우 CLI 가 작동하지 않을 수 있다.
> 이 경우에 `winpty python.exe`로 실행하면 제대로 작동한다.
> `alias python='winpty python.exe'` 를 `vi ~/.bashrc` 로 하여 저장해두면 편하다.


## 4. 프로젝트 시작하기

```sh
$ django-admin startproject mysite
```

위와 같이 실행하면 mysite 라는 디렉토리가 만들어진다.
 
mysite라는 디렉토리에 또 mysite 라는 디렉토리가 있고 아래와 같은 파일이 생성되었다.    

```sh
__init__.py  settings.py  urls.py  wsgi.py
```

설정 및 개발 서버 실행에 대한 부분은 다음에 포스팅할 예정이다.
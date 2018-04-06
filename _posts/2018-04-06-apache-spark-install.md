---
layout: post
title:  "Ubuntu Linux에 Apache Spark 설치"
date:   2018-04-06 16:27:00 +0900
tags:
- Ubuntu
- Spark
- Apache
- Linux
---

# Ubuntu 에 Apache Spark 설치

## 1. 다운로드

### 1. Apache Spark 홈페이지 방문
[Apache Spark 다운로드 페이지](http://spark.apache.org/downloads.html) 에서 Spark Release와 package를 선택한 후 DownLoad Spark 를 눌러 다운로드 한다.

나는 2.3.0 (Feb 28 2018) 릴리즈의 Pre-built for Apache Hadoop 2.7 and later 패키지 타입으로 다운로드 받았다.

### 2. 압축 해제

```sh
$ tar -xf spark-2.3.0-bin-hadoop2.7.tgz
$ cd spark-2.3.0-bin-hadoop2.7
```

압축을 해제한 후 디렉토리에 들어가면 여러 파일들을 담고있다.

간략하게 설명하면,

- README.md : Apache Spark 소개

- bin : Spark에서 사용하는 실행 파일

- core, streaming, python 등 : Spark 주요 컴포넌트의 소스 코드

- examples : 사용자들에게 보여주기 위한 예제 코드


## 2. 셸 접속하기

### 1. 파이썬 셸

```sh
$ bin/pyspark
```


### 2. 스칼라 셸

```sh
$ bin/spark-shell
```


### 3. 셸 실행 중 오류 대응

```sh
JAVA_HOME is not set
```
위와 같은 메시지가 뜨는 경우에는 jdk를 설치해준다.
Spark 자체가 자바 가상 머신 위에서 돌아간다. (스칼라로 만들어졌지만 스칼라란 언어 자체가 컴파일하면 자바 바이트 코드로 변환되기 때문)

```sh
$ sudo apt install openjdk-8-jdk
혹은
$ export JAVA_HOME=자바설치경로
```

jdk, jre가 설치되어있다면 해당 경로로 JAVA_HOME 변수를 환경변수로 지정해주고, 그것이 아니라면 jdk를 설치해준다.


```sh
Python 2.7.12 (default, Nov 20 2017, 18:23:56) 
[GCC 5.4.0 20160609] on linux2
Type "help", "copyright", "credits" or "license" for more information.
Error: A JNI error has occurred, please check your installation and try again
Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException: 64
	at java.util.jar.JarFile.match(java.base@9-internal/JarFile.java:983)
	at java.util.jar.JarFile.checkForSpecialAttributes(java.base@9-internal/JarFile.java:1017)
	.............
```

위와 같은 에러가 뜬다면 java 버전을 spark가 인지하지 못했기 때문이다.

일단 quit() 를 입력하여 셸에서 빠져나온 뒤

```sh
sudo update-java-alternatives -s java-1.8.0-openjdk-amd64
```

나는 java 1.8.0 버전을 설치하였으므로 위와 같은 명령어로 해결하였다.


## 3. 셸 실행 시 로그 메시지 줄이기

```sh
$ vi conf/log4j.properties.template
```

위의 파일을 열어

```sh
log4j.rootCategory=INFO, console
```

위 부분을

```sh
log4j.rootCategory=WARN, console
```

으로 수정하여 로깅 레벨을 낮춰준다.

다시 셸을 열면 더욱 적은 로그가 출력된다.

## 4. 파이썬으로 줄 수 세기 예제

Spark 에서는 연산 과정을 클러스터 전체에 걸쳐 자동으로 병렬화해 분산 배치된 연산 작업들의 모음으로 표현한다. 

이 모음은 RDD(Resilient Distributed Dataset)이라고 부른다.

```python
>>> lines = sc.textFile("README.md") # lines 라는 RDD를 선언한다.
>>> lines.count() # RDD의 아이템 개수를 센다
103
>>> lines.first() # 이 RDD의 첫번째 아이템을 출력한다. (README.md의 첫번째 라인)
'# Apache Spark'
```

위의 예제를 통해 Spark 로컬 머신으로 변수에 RDD를 만들고 개수를 세거나 첫번째 아이템을 출력해보았다.

## 출처

- [O'REILLY Leaning Spark 도서](http://shop.oreilly.com/product/0636920028512.do)

- https://docs.oracle.com/cd/E19182-01/820-7851/inst_cli_jdk_javahome_t/

- https://stackoverflow.com/questions/34353556/spark-java-error-in-standalone-application
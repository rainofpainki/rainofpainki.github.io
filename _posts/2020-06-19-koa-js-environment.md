---
layout: post
title:  "Windows 10에 Node.js / Koa.js / TypeScript 개발 환경 설치"
date:   2020-06-19 17:18:00 +0900
tags:
- Windows
- Node.js
- TypeScript
- Koa.js
- mysql
---


# 1. NVM 설치
## 1.1. [다운로드](https://github.com/coreybutler/nvm-windows/releases)하여 설치
## 1.2. 시스템-환경변수(사용자변수-Path)에 추가 
> ex) C:\Users\`rainofpainki`\AppData\Roaming\nvm 

# 2. Node.js 설치
## 2.1. Windows Powershell 실행 *(관리자 권한으로 실행)*
## 2.2. Node.js 설치 *(20.06.17 당시 최신LTS 12.18.0)*
```bash
$ nvm install v12.18.0
```
## 2.3. Node.js 버전 확인
```bash
$ nvm ls
```
## 2.4. 사용할 Node.js 버전 선택
```bash
$ nvm use 12.18.0
```
## 2.5. 설치 확인
```bash
$ node -v
$ npm -v
```

# 3. Chocolatey 설치
## 3.1. Windows Powershell 실행 (관리자 권한으로 실행)
## 3.2. 아래 커맨드 실행
```bash
$ Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
```
## 3.3. 설치 확인

```bash
$ choco
$ choco -?
```

# 4. Yarn 설치
## 4.1. Windows Powershell 실행 (관리자 권한으로 실행)
## 4.2. choco 이용하여 yarn 설치 
```bash
$ choco install yarn
```
## 4.3. 설치 확인
```
$ refreshenv # 환경변수 초기화
$ yarn -v
```

# 5. Koa.js 프로젝트 생성
## 5.1. 원하는 경로에 Workspace 생성
```bash
$ cd ~
$ cd workspace
```
## 5.2. 형상관리 원격 저장소에 project 생성하고 git clone
```bash
$ git config --global user.name "rainofpainki"
$ git config --global user.email "rainofpainki@naver.com"
$ git clone {git clone url}
```

## 5.3. $ cd firstmall-api
```bash
$ yarn init
# 아래와 같이 적절하게 설정
question name (koa-js-test):
question version (1.0.0): 
question description: koa.js test
question entry point (index.js): 
question repository url: 
question author: rainofpainki
question license (MIT): 
question private: 
```
## 5.4. koa 모듈 설치 
```bash
$ yarn add koa
```
## 5.5. ESLint 설정
### 5.5.1. npm bin 폴더 전역변수 설정
```bash
$ npm bin -g
```
출력되는 폴더를 시스템-환경변수에 추가

```bash
$ npm bin
```
출력되는 폴더를 시스템-환경변수에 추가

```bash
$ refreshenv
$ Get-ExecutionPolicy
```
권한이 RemoteSigned가 아니라면 아래와 같은 명령어 실행

```bash
$ Set-ExecutionPolicy RemoteSigned
```

### 5.5.2. 전역에 ESLint 설치
```bash
$ npm install -g eslint
```

### 5.5.3. eslint 설정
```bash
$ eslint --init
? How would you like to use ESLint? To check syntax, find problems, and enforce code style
? What type of modules does your project use? JavaScript modules (import/export)
? Which framework does your project use? None of these? Does your project use TypeScript? Yes
? Where does your code run? Node? How would you like to define a style for your project? Use a popular style guide
? Which style guide do you want to follow? [Standard:](https://github.com/standard/standard) 
? What format do you want your config file to be in? JSON
```
.eslintrc.json 생성 확인

### 5.5.4. (vscode 이용시에만) VSCode 실행하여 MarketPlace에서 ESLint, npm 설치

# 6. Koa.js 기본 사용법
## 6.1. src/index.js 디렉토리 및 파일 생성
## 6.2. 파일 내용에 아래와 같이 추가
```javascript
const Koa = require('koa');
const app = new Koa();

app.use(ctx => {
    ctx.body = 'Hello Koa';
});

app.listen(4000, () => {
    console.log('node server is listening to port 4000');
});
```

## 6.3. 서버 실행
```bash
$ node src
```

[localhost](http://localhost:4000/) 접속하여 확인

# 7. TypeScript 적용 방법

## 7.1. typescript 관련 npm 모듈 설치 

```bash
$ npm i --save-dev typescript ts-node nodemon @types/koa @types/node
$ npm i --save-dev eslint eslint-config-prettier @typescript-eslint/parser
```

## 7.2. 해당 workspace에서 실행
```bash
$ tsc --init
```

## 7.3. package.json 에 main 속성을 index.js 를 index.ts로 변경
## 7.4. tsconfig.js (있으면) 삭제
## 7.5. tsconfig.json 에 아래와 같이 저장
```json
{
  "compilerOptions": {
    "outDir": "dist",
    "target": "es2017",
    "module": "commonjs",
    "sourceMap": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "resolveJsonModule": true,
    "typeRoots": [
      "node_modules/@types"
    ]
  },
  "include": [
    "src/**/**.ts",
    "test/**/**.ts"
  ],
  "exclude": [
    "node_modules"
  ]
}
```

## 7.6. src/index.ts 아래 내용으로 저장
```typescript
import * as Koa from 'koa'
import { Context } from 'koa'

const app = new Koa()

app.use((ctx: Context) => {
  ctx.body = 'Hello Koa'
})

app.listen(4000, () => {
  console.log('node server is listening to port 4000')
})
```

## 7.7. 실행 확인
```bash 
$ tsc && node dist/index.js
```
 
또는

```bash
$ ts-node src
```
로 실행 후, [localhost](http://localhost:4000/) 접속하여 확인

# 8. choco 이용하여 MySQL 설치 (부록)
## 8.1. Windows Powershell 실행 (관리자 권한으로 실행)
## 8.2. choco 이용하여 설치 
```bash
$ choco install mysql --params "/port:3306 /serviceName:MySQL"
```
## 8.3. Powershell 재실행
```bash
$ mysql // access denied 뜨면 아래 실행
$ mysql_secure_installation
```

## 8.4. 접속
 
```bash
$ mysql -uroot -p
```

## 8.5. 사용자/데이터베이스 생성

```bash
CREATE USER 'rainofpainki'@'localhost' IDENTIFIED BY 'rainofpainki';
GRANT USAGE ON *.* TO 'rainofpainki'@'localhost';
FLUSH PRIVILEGES;
CREATE DATABASE `koa-js-db`;
GRANT EXECUTE, SELECT, SHOW VIEW, ALTER, ALTER ROUTINE, CREATE, CREATE  ROUTINE, CREATE TEMPORARY TABLES, CREATE VIEW, DELETE, DROP, EVENT,  INDEX, INSERT, REFERENCES, TRIGGER, UPDATE, LOCK TABLES  ON  `koa-js-db`.* TO 'rainofpainki'@'localhost' WITH GRANT OPTION;
FLUSH PRIVILEGES;
```


# 9. Ref

https://code-masterjung.tistory.com/46

https://backend-intro.vlpt.us/1/01.html

https://novemberde.github.io/node/2017/10/22/Express-Typescript.html

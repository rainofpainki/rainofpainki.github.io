---
layout: post
title:  "How to color the text in Bash"
date:   2018-02-02 14:15:00 +0900
categories: Linux Bash Color Shell ShellScript
---

# 리눅스 터미널에서 텍스트에 색깔 입히기

## 1. 명령어별 색깔 설정 확인하기

```sh
$ dircolors

LS_COLORS='rs=0:di=01;34:ln=01;36:mh=00:pi=40;33:so=01;35:do=01;35:bd=40;33;01:cd=40;33;01:or=40;31;01:mi=00:su=37;41:sg=30;43:ca=30;41:tw=30;42:ow=34;42:st=37;44:ex=01;32:*.tar=01;31:*.tgz=01;31:*.arc=01;31:*.arj=01;31:*.taz=01;31:*.lha=01;31:*.lz4=01;31:*.lzh=01;31:*.lzma=01;31:*.tlz=01;31:*.txz=01;31:*.tzo=01;31:*.t7z=01;31:*.zip=01;31:*.z=01;31:*.Z=01;31:*.dz=01;31:*.gz=01;31:*.lrz=01;31:*.lz=01;31:*.lzo=01;31:*.xz=01;31:*.bz2=01;31:*.bz=01;31:*.tbz=01;31:*.tbz2=01;31:*.tz=01;31:*.deb=01;31:*.rpm=01;31:*.jar=01;31:*.war=01;31:*.ear=01;31:*.sar=01;31:*.rar=01;31:*.alz=01;31:*.ace=01;31:*.zoo=01;31:*.cpio=01;31:*.7z=01;31:*.rz=01;31:*.cab=01;31:*.jpg=01;35:*.jpeg=01;35:*.gif=01;35:*.bmp=01;35:*.pbm=01;35:*.pgm=01;35:*.ppm=01;35:*.tga=01;35:*.xbm=01;35:*.xpm=01;35:*.tif=01;35:*.tiff=01;35:*.png=01;35:*.svg=01;35:*.svgz=01;35:*.mng=01;35:*.pcx=01;35:*.mov=01;35:*.mpg=01;35:*.mpeg=01;35:*.m2v=01;35:*.mkv=01;35:*.webm=01;35:*.ogm=01;35:*.mp4=01;35:*.m4v=01;35:*.mp4v=01;35:*.vob=01;35:*.qt=01;35:*.nuv=01;35:*.wmv=01;35:*.asf=01;35:*.rm=01;35:*.rmvb=01;35:*.flc=01;35:*.avi=01;35:*.fli=01;35:*.flv=01;35:*.gl=01;35:*.dl=01;35:*.xcf=01;35:*.xwd=01;35:*.yuv=01;35:*.cgm=01;35:*.emf=01;35:*.ogv=01;35:*.ogx=01;35:*.aac=00;36:*.au=00;36:*.flac=00;36:*.m4a=00;36:*.mid=00;36:*.midi=00;36:*.mka=00;36:*.mp3=00;36:*.mpc=00;36:*.ogg=00;36:*.ra=00;36:*.wav=00;36:*.oga=00;36:*.opus=00;36:*.spx=00;36:*.xspf=00;36:';
export LS_COLORS
```

dircolors 라는 명령어를 입력하면 각 명령어들이 어떤 색깔로 출력되는지에 대한 설정 내용을 알 수 있다.
어떤 값이 어떤 색상일까?

## 2. 색상 코드표


| 얇게 | 색깔 | 굵게 | 색깔 |
|-----------|------------|-----------|--------------|
| 30 | Black | 1;30 | Dark Gray |
| 31 | Red | 1;31 | Dark Red |
| 32 | Green | 1;32 | Dark Green |
| 33 | Brown | 1;33 | Yellow |
| 34 | Blue | 1;34 | Dark Blue |
| 35 | Magenta | 1;35 | Dark Magenta |
| 36 | Cyan | 1;36 | Dark Cyan |
| 37 | Light Gray | 1;37 | White |


## 3. 사용 방법

```sh
$ echo -e "\033[31mTEST\033[0m"
# 또는
$ echo -e "\e[31mTEST\e[0m"
# \033을 \e로 바꿔도 동일하게 동작한다.
```

![사진1](https://raw.githubusercontent.com/rainofpainki/rainofpainki.github.io/master/assets/img/shell_text_color/01.PNG)


위에서 보면 31 부분을 위의 표에서 원하는 색깔로 바꿔주면 된다. 글자를 굵게 하고 싶다면 1;31 과 같은 방식으로 사용하면 된다.

\e[0m 을 하는 이유는 색깔을 원래대로 다시 돌려놓기 위해서이다. 

> echo 시 -e 옵션을 붙여야 백슬래시 문자를 허용한다.


## 4. 배경 색상표

| Color | Background |
|---------|------------|
| Black | 40 |
| Red | 41 |
| Green | 42 |
| Yellow | 43 |
| Blue | 44 |
| Magenta | 45 |
| Cyan | 46 |
| White | 47 |


## 5. 배경 사용법

배경을 사용하고 싶다면 앞에 배경색 값을 넣으면 된다.

```sh
# 배경 넣고 얇게
$ echo -e "\e[43;31mTEST\e[0m"

# 배경 넣고 굵게
$ echo -e "\e[43;1;31mTEST\e[0m"
```

![사진2](https://raw.githubusercontent.com/rainofpainki/rainofpainki.github.io/master/assets/img/shell_text_color/02.PNG)
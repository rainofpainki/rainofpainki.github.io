---
layout: post
title:  "CentOS가 Ubuntu 보다 더 안정적인 이유"
date:   2018-05-03 16:25:00 +0900
tags:
- Ubuntu
- CentOS
- Linux
---

## 1. 개요

Ubuntu와 CentOS를 비교하는 글을 많이 보았다. 

명확하고 확실한, 그러니까 `기술적으로 어떤 것이 낫다.` 라는 대답은 찾기 어려웠다.

조금 더 검색하다 보면 아래와 같은 정보를 얻을 수 있다.

> CentOS가 안정성이 더 뛰어나서 실무에 적합하고,
> Ubuntu가 신규 패키지, 컴포넌트 등에 대한 대응이 빨라서 테스트용으로 적합하다.

하지만 어떤 면에서 (기술적으로) 안정성이 더 뛰어나다는 근거는 없었다.

CentOS가 안정성이 뛰어나다고 하지만 `어떤 기술적인 면에서 어떻게 설계가되어 안정성이 뛰어나다`라는 대답은 없었고, 개인적은 생각으로는 Ubuntu도 충분히 안정적인 소프트웨어라고 생각한다. 

하지만 Ubuntu 공식 홈페이지와 CentOS 공식 홈페이지에서 그 대답과 비슷한 것을 찾을 수 있었다.

## 2. 유지관리 기간

### 2.1. Ubuntu

![LTS 버전의 정보](https://raw.githubusercontent.com/rainofpainki/rainofpainki.github.io/master/assets/img/ubuntu_vs_centos/01.PNG "https://wiki.ubuntu.com/LTS")

![Release 정보](https://raw.githubusercontent.com/rainofpainki/rainofpainki.github.io/master/assets/img/ubuntu_vs_centos/02.PNG "https://wiki.ubuntu.com/Releases")

Ubuntu Regular (정식 릴리즈) 의 경우 신규 출시한 버전은 9개월간 유지 관리가 된다.

Ubuntu LTS (Long Term Support) 의 경우 Flavors[^1]를 제외하고 Ubuntu Desktop은 3년, Ubuntu Server는 5년 간 지원이 된다.

릴리즈는 예정된 일정에 따라 약 6개월간 업데이트 된다.

### 2.1. CentOS

![CentOS Wiki 홈페이지](https://raw.githubusercontent.com/rainofpainki/rainofpainki.github.io/master/assets/img/ubuntu_vs_centos/03.PNG "https://wiki.centos.org/")

반면, CentOS는 보안 업데이트를 통해 최대 10년 동안 유지 관리된다. (Red Hat의 지원 기간은 출시 버전에 따라 다양함)

새로운 CentOS 버전은 약 2년마다 출시되며, 각 CentOS 버전은 최신 하드웨어를 지원할 수 있도록 주기적으로 (약 6개월 마다) 업데이트 된다.


## 3. 결론

결론적으로 CentOS가 안정적이라 라는 것은 유지 관리 기간이 길기 때문이다.

필자는 과거에 CentOS를 사용하다가 현재 Ubuntu를 주로 사용하는데 서버용 OS를 선택할 때 유지관리 기간도 고려하여 선택하는 것이 좋겠다.

개인적인 생각으로는 Desktop을 쓸 것이라면 Ubuntu Desktop을 사용하고, (물론 Fedora를 유료로 구매할 생각이 있다면 Fedora도 좋다) 장기간 서비스해야 할 서버용 OS를 선택할 것이라면 CentOS가 더 나을 수 있겠다.  


## 4. Ref

1) https://wiki.ubuntu.com/LTS

2) https://wiki.ubuntu.com/Releases

3) https://wiki.centos.org

4) https://www.quora.com/Is-CentOS-really-better-than-Ubuntu-as-a-server-or-is-it-just-marketing

5) https://www.quora.com/What-are-the-main-differences-between-CentOS-and-Ubuntu-Linux-operating-systems

\[^1]: Ubuntu의 다양한 커스텀 버전. [이곳](https://wiki.ubuntu.com/UbuntuFlavors)을 참고하자.
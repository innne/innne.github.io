---
layout: post
title: OverTheWire - Bandit (Level 2)
date: 2021-01-08 19:00:00 +0900
category: System_Hacking
---


# Bandit (Level 2)

#### 홈 디렉토리에 있는 "spaces in this filename" 파일을 통해 다음 단계(Level 3)로 가는 비밀번호 알아내기

<br/>


> 접속해야 할 주소:  bandit.labs.overthewire.org
>
> 포트 번호: 2220
>
> 계정명: bandit2
>
> 비밀번호: CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9
>
> 필요한 명령어: ls, cd, cat, file, du, find

<br/>

이전 단계(Level 1)에서  구한 비밀번호를 입력하여 로그인 한다.

```shell
ssh -p 2220 bandit2@bandit.labs.overthewire.org
```

<br/>

file 명령어를 통해 "spaces in thie filename" 파일은 ASCII text 파일임을 알 수 있다.

```shell
file ./*
```

<br/>

ls 명령어로  파일 목록을 확인한 후, cat 명령어를 통해 "spaces in this filename" 파일을 읽어보자. 

만약에 "cat ./spaces in this filename" 이라고 입력하면 "spaces", "in", "this", "filename" 이라는 총 4개의 파일을 오픈하려고 하기 때문에 오류가 발생한다.

<br/>

 그러므로 공백 문자 좌측에 역 슬래시(\\)를 입력하여 그것이 공백 문자임을 표현하거나 쌍따옴표를 이용해서 파일의 풀네임을 정확하게 입력한다.

```shell
ls -al
cat ./spaces\ in\ this\ filename
cat ./"spaces in this filename"
```

![bandit3_1](/public/img/bandit3_1.PNG)

<br/>

다음 단계(Level 3)로 넘어가기 위한 비밀번호를 알 수 있다.

```shell
UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK
```


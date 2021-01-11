---
layout: post
title: OverTheWire - Bandit (Level 3)
date: 2021-01-11 19:00:00 +0900
category: System_Hacking
---


# Bandit (Level 3)

#### 'inhere' 디렉토리에 있는 숨김 파일을 통해 다음 단계(Level 4)로 가는 비밀번호 알아내기

<br/>


> 접속해야 할 주소:  bandit.labs.overthewire.org
>
> 포트 번호: 2220
>
> 계정명: bandit3
>
> 비밀번호: UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK
>
> 필요한 명령어: ls, cd, cat, file, du, find

<br/>

이전 단계(Level 2)에서 구한 비밀번호를 입력하여 로그인 한다.

```shell
ssh -p 2220 bandit3@bandit.labs.overthewire.org
```

<br/>

ls 명령어로 'inhere' 디렉토리를 확인한 후, cd 명령어를 통해 해당 디렉토리로 들어가자. 

그리고 cat 명령어를 통해 '.'으로 시작하는 숨김파일을 읽어보자.

```shell
ls -al
cd ./inhere
```

![bandit3_1](/public/img/bandit3_1.PNG) 

![bandit3_2](/public/img/bandit3_2.PNG) 

<br/>

다음 단계(Level 4)로 넘어가기 위한 비밀번호를 알 수 있다.

```shell
pIwrPrtPN36QITSp3EQaw936yaFoFgAB
```


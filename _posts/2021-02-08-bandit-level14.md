---
layout: post
title: OverTheWire - Bandit (Level 14)
date: 2021-02-08 14:00:00 +0900
category: System_Hacking
---


# Bandit (Level 14)

####  현재 단계의 비밀번호를 localhost의 30000번 포트로 제출하여 다음 단계(Level 15)로 가는 비밀번호 알아내기

<br/>


> 접속해야 할 주소:  bandit.labs.overthewire.org
>
> 포트 번호: 2220
>
> 계정명: bandit14
>
> 비밀번호: 4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e
>
> 필요한 명령어: ssh, telnet, nc, openssl, s_client, nmap

<br/>

이전 단계(Level 13)에서 구한 비밀번호를 입력하여 로그인 한다.

```shell
ssh -p 2220 bandit14@bandit.labs.overthewire.org
```

<br/>

ls 명령어를 통해 파일들을 확인할 수 있다.

```shell
ls -al
```

![bandit14_1](/public/img/bandit14_1.PNG) 

<br/>

nmap을 이용하여 포트스캐닝을 해보면 30000번 포트가 열려있는 것을 알 수 있다.

```shell
nmap -p 1-1024 127.0.0.1
nmap -p 20000-40000 127.0.0.1
```

![bandit14_2](/public/img/bandit14_2.PNG)

![bandit14_3](/public/img/bandit14_3.PNG) 

<br/>

nc를 이용해 localhost(127.0.0.1)에 접속한 후, 현재 단계의 비밀번호를 입력하자.

```shell
nc 127.0.0.1 30000
4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e
```

![bandit14_4](/public/img/bandit14_4.PNG) 

<br/>

다음 단계(Level 15)로 넘어가기 위한 비밀번호를 알 수 있다.

```shell
BfMYroe26WYalil77FoDi9qh59eK5xNr
```

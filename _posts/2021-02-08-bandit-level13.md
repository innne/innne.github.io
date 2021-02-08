---
layout: post
title: OverTheWire - Bandit (Level 13)
date: 2021-02-08 13:00:00 +0900
category: System_Hacking
---


# Bandit (Level 13)

####  /etc/bandit_pass/bandit14에 저장되어 있고, 'bandit14' 계정만 읽을 수 있는 다음 단계(Level 14)로 가는 비밀번호 알아내기

<br/>


> 접속해야 할 주소:  bandit.labs.overthewire.org
>
> 포트 번호: 2220
>
> 계정명: bandit13
>
> 비밀번호: 8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL
>
> 필요한 명령어: ssh, telnet, nc, openssl, s_client, nmap

<br/>

이전 단계(Level 12)에서 구한 비밀번호를 입력하여 로그인 한다.

```shell
ssh -p 2220 bandit13@bandit.labs.overthewire.org
```

<br/>

ls 명령어를 통해 'sshkey.private'파일을 확인할 수 있다. 

```shell
ls -al
```

![bandit13_1](/public/img/bandit13_1.PNG) 

<br/>

추가로 file 명령어를 통해 보면 key가 들어있는 파일임을 알 수 있다.

```shell
file ./sshkey.private
```

![bandit13_2](/public/img/bandit13_2.PNG)

<br/>

ssh를 통해 bandit14로 접속하기 위해서는 비밀번호가 필요하다.

하지만 우린 'sshkey.private' 파일을 이용하여 접속할 수 있다.

```shell
ssh -i ./sshkey.private bandit14@localhost
```

![bandit13_3](/public/img/bandit13_3.PNG) 

<br/>

이제 /etc/bandit_pass/bandit14 파일을 읽어보자.

```shell
cat /etc/bandit_pass/bandit14
```

![bandit13_4](/public/img/bandit13_4.PNG) 

<br/>

다음 단계(Level 14)로 넘어가기 위한 비밀번호를 알 수 있다.

```shell
4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e
```




---
layout: post
title: OverTheWire - Bandit (Level 0)
date: 2021-01-05 15:00:00 +0900
category: System_Hacking
---


# Bandit (Level 0)

#### SSH를 통해 게임에 로그인 한 후, readme 파일을 통해 다음 단계(Level 1)로 가는 비밀번호 알아내기

<br/>


> 접속해야 할 주소:  bandit.labs.overthewire.org
>
> 포트 번호: 2220
>
> 계정명: bandit0
>
> 비밀번호: bandit0
>
> 필요한 명령어: ssh, ls, cd, cat, file, du, find

<br/>

ssh 명령어를 이용하여 로그인 한다.

```shell
ssh -p 2220 bandit0@bandit.labs.overthewire.org
```

![bandit0_1](/public/img/bandit0_1.PNG)

<br/>

비밀번호 bandit0을 입력하면 로그인 성공!

![bandit0_2](/public/img/bandit0_2.PNG)

<br/>

ls 명령어로 파일 목록을 확인한 후, cat 명령어를 통해 readme 파일을 읽어보자.

```shell
ls -al
cat readme
```

![bandit0_3](/public/img/bandit0_3.PNG)

<br/>

다음 단계(Level 1)로 넘어가기 위한 비밀번호를 알 수 있다.

```shell
boJ9jbbUNNfktd78OOpsqOltutMc3MY1
```


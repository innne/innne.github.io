---
layout: post
title: OverTheWire - Bandit (Level 1)
date: 2021-01-05 16:20:00 +0900
category: System_Hacking
---


# Bandit (Level 1)

#### 홈 디렉토리에 있는 이름이 '-'인 파일을 통해 다음 단계(Level 2)로 가는 비밀번호 알아내기

<br/>


> 접속해야 할 주소:  bandit.labs.overthewire.org
>
> 포트 번호: 2220
>
> 계정명: bandit1
>
> 비밀번호: boJ9jbbUNNfktd78OOpsqOltutMc3MY1
>
> 필요한 명령어: ls, cd, cat, file, du, find

<br/>

이전 단계(Level 0)에서  구한 비밀번호를 입력하여 로그인 한다.

```shell
ssh -p 2220 bandit1@bandit.labs.overthewire.org
```

<br/>

ls 명령어로  파일 목록을 확인한 후, cat 명령어를 통해 '-' 파일을 읽어보자.

리눅스 시스템에서는 '-'를 명령어의 인자로 보기 때문에, 상대경로나 절대경로로 표현하여 '-'를 파일 이름으로 인식하도록 한다.

```shell
ls -al
cat ./-
cat /home/bandit1/-
```

![bandit1_1](/public/img/bandit1_1.PNG)

<br/>

다음 단계(Level 2)로 넘어가기 위한 비밀번호를 알 수 있다.

```shell
CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9
```


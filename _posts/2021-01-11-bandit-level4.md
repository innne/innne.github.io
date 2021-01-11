---
layout: post
title: OverTheWire - Bandit (Level 4)
date: 2021-01-11 19:30:00 +0900
category: System_Hacking
---


# Bandit (Level 4)

#### 'inhere' 디렉토리에 있는 사람이 읽을 수 있는 어느 한 파일을 통해 다음 단계(Level 5)로 가는 비밀번호 알아내기

<br/>


> 접속해야 할 주소:  bandit.labs.overthewire.org
>
> 포트 번호: 2220
>
> 계정명: bandit4
>
> 비밀번호: pIwrPrtPN36QITSp3EQaw936yaFoFgAB
>
> 필요한 명령어: ls, cd, cat, file, du, find

<br/>

이전 단계(Level 3)에서 구한 비밀번호를 입력하여 로그인 한다.

```shell
ssh -p 2220 bandit4@bandit.labs.overthewire.org
```

<br/>

ls 명령어로 'inhere' 디렉토리를 확인한 후, cd 명령어를 통해 해당 디렉토리로 들어가자. 

```shell
ls -al
cd ./inhere
```

![bandit4_1](/public/img/bandit4_1.PNG) 

<br/>

'inhere' 디렉토리에는 10개의 파일이 있으며 file 명령어를 통해 확인하니 이 중 9개는 data파일이고 1개는 ASCII text 파일이다.

```shell
ls -al
file ./*
```

 ![bandit4_2](/public/img/bandit4_2.PNG) 

<br/>

cat 명령어를 통해 읽어보면 ASCII text 파일인 '-file07' 만 읽을 수 있고 다른 data 파일들은 일반적으로 사람이 읽을 수 없는 형태로 되어있다는 것을 알 수 있다.

 ![bandit4_3](/public/img/bandit4_3.PNG) 

<br/>

다음 단계(Level 5)로 넘어가기 위한 비밀번호를 알 수 있다.

```shell
koReBOKuIDDepwhWk7jZC0RTdopnAYKh
```


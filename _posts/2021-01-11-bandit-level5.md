---
layout: post
title: OverTheWire - Bandit (Level 5)
date: 2021-01-11 20:00:00 +0900
category: System_Hacking
---


# Bandit (Level 5)

#### 'inhere' 디렉토리 내부 어딘가에 있는 파일(사람이 읽기 가능, 크기1033 bytes, 비 실행파일)을 통해 다음 단계(Level 6)로 가는 비밀번호 알아내기

<br/>


> 접속해야 할 주소:  bandit.labs.overthewire.org
>
> 포트 번호: 2220
>
> 계정명: bandit5
>
> 비밀번호: koReBOKuIDDepwhWk7jZC0RTdopnAYKh
>
> 필요한 명령어: ls, cd, cat, file, du, find

<br/>

이전 단계(Level 4)에서 구한 비밀번호를 입력하여 로그인 한다.

```shell
ssh -p 2220 bandit5@bandit.labs.overthewire.org
```

<br/>

ls 명령어로 'inhere' 디렉토리를 확인한 후, cd 명령어를 통해 해당 디렉토리로 들어가자. 

```shell
ls -al
cd ./inhere
```

![bandit5_1](/public/img/bandit5_1.PNG) 

<br/>

'inhere' 디렉토리 내부에는 20개의 디렉토리가 있으며, 각 디렉토리에는 여러 파일들이 있다. 

![bandit5_2](/public/img/bandit5_2.PNG) 

![bandit5_2-2](/public/img/bandit5_2-2.PNG) 

<br/>

find 명령어를 통해 파일의 크기가 1033 bytes인 파일을 찾아보자.

```shell
find . -size 1033c
```

 ![bandit5_3](/public/img/bandit5_3.PNG) 

<br/>

'maybehere07' 디렉토리에 있는 '.file2' 파일을 정확하게 확인해보면 파일의 크기가 1033 bytes이고 실행파일이 아니며, 사람이 읽을 수 있는 ASCII text 파일임을 알 수 있다.

그리고 cat 명령어를 통해 해당 파일을 읽어보자.

 ![bandit5_4](/public/img/bandit5_4.PNG) 

<br/>

다음 단계(Level 6)로 넘어가기 위한 비밀번호를 알 수 있다.

```shell
DXjZPULLxYr17uwoI01bNLQbtFemEgo7
```


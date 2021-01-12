---
layout: post
title: OverTheWire - Bandit (Level 9)
date: 2021-01-12 14:30:00 +0900
category: System_Hacking
---


# Bandit (Level 9)

#### 'data.txt' 파일 속 몇 개의 '=' 문자로 시작하며 읽을 수 있는 글자 중 하나인 다음 단계(Level 10)로 가는 비밀번호 알아내기

<br/>


> 접속해야 할 주소:  bandit.labs.overthewire.org
>
> 포트 번호: 2220
>
> 계정명: bandit9
>
> 비밀번호: UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR
>
> 필요한 명령어: grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd

<br/>

이전 단계(Level 8)에서 구한 비밀번호를 입력하여 로그인 한다.

```shell
ssh -p 2220 bandit9@bandit.labs.overthewire.org
```

<br/>

ls 명령어를 통해 data.txt 파일을 찾을 수 있다. 

```shell
ls -al
```

![bandit9_1](/public/img/bandit9_1.PNG) 

<br/>

추가로 file 명령어를 통해 파일의 형식을 보면 data 파일로, 일반적으로 사람이 읽을 수 없는 형태로 되어있다.

```shell
file ./data.txt
```

![bandit9_2](/public/img/bandit9_2.PNG)

<br/>

'=' 문자로 시작한다고 했으므로 grep 명령어를 이용해 읽어보았지만 나오지 않는다.

![bandit9_3](/public/img/bandit9_3.PNG) 

<br/>

그러므로 data 형식을 사람이 읽을 수 있는 string 형식으로 변경한 후, grep 명령어로 확인해보자.

```shell
strings ./data.txt | grep =
```

![bandit9_4](/public/img/bandit9_4.PNG) 

<br/>

다음 단계(Level 10)로 넘어가기 위한 비밀번호를 알 수 있다.

```shell
truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk
```




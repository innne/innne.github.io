---
layout: post
title: OverTheWire - Bandit (Level 10)
date: 2021-01-18 22:00:00 +0900
category: System_Hacking
---


# Bandit (Level 10)

#### 'data.txt' 파일에서 base64로 인코딩 되어있는 다음 단계(Level 11)로 가는 비밀번호 알아내기

<br/>


> 접속해야 할 주소:  bandit.labs.overthewire.org
>
> 포트 번호: 2220
>
> 계정명: bandit10
>
> 비밀번호: truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk
>
> 필요한 명령어: grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd

<br/>

이전 단계(Level 9)에서 구한 비밀번호를 입력하여 로그인 한다.

```shell
ssh -p 2220 bandit10@bandit.labs.overthewire.org
```

<br/>

ls 명령어를 통해 data.txt 파일을 찾을 수 있다. 

```shell
ls -al
```

![bandit10_1](/public/img/bandit10_1.PNG) 

<br/>

추가로 file 명령어를 통해 파일의 형식을 보면 ASCII text 파일이다.

```shell
file ./data.txt
```

![bandit10_2](/public/img/bandit10_2.PNG)

<br/>

cat 명령어를 통해 파일의 내용을 읽어보면 base64로 인코딩 되어있는 비밀번호를 확인할  수 있다.

참고로, 문자열 끝에 '==' 기호가 있다면 base64로 인코딩 된 것이라고 예상할 수 있다.

![bandit10_3](/public/img/bandit10_3.PNG) 

<br/>

리눅스에는 기본적으로 base64라는 프로그램이 설치되어 있으므로 manual 페이지를 통해 명령어 사용법을 확인한 후 디코딩하자.

```shell
man base64
base64 -d ./data.txt
cat ./data.txt | base64 -d
```

![bandit10_4](/public/img/bandit10_4.PNG) 

<br/>

다음 단계(Level 11)로 넘어가기 위한 비밀번호를 알 수 있다.

```shell
IFukwKGsFW8MOq3IRFqrxE1hxTNEbUPR
```




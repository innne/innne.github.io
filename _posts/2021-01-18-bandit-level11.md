---
layout: post
title: OverTheWire - Bandit (Level 11)
date: 2021-01-18 22:30:00 +0900
category: System_Hacking
---


# Bandit (Level 11)

#### 'data.txt' 파일에서 모든 소문자 및 대문자가 위치상으로 13자리  이동되었을 때, 다음 단계(Level 12)로 가는 비밀번호 알아내기

<br/>


> 접속해야 할 주소:  bandit.labs.overthewire.org
>
> 포트 번호: 2220
>
> 계정명: bandit11
>
> 비밀번호: IFukwKGsFW8MOq3IRFqrxE1hxTNEbUPR
>
> 필요한 명령어: grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd

<br/>

이전 단계(Level 10)에서 구한 비밀번호를 입력하여 로그인 한다.

```shell
ssh -p 2220 bandit11@bandit.labs.overthewire.org
```

<br/>

ls 명령어를 통해 data.txt 파일을 찾을 수 있다. 

```shell
ls -al
```

![bandit11_1](/public/img/bandit11_1.PNG) 

<br/>

추가로 file 명령어를 통해 파일의 형식을 보면 ASCII text 파일이다.

```shell
file ./data.txt
```

![bandit11_2](/public/img/bandit11_2.PNG)

<br/>

cat 명령어를 통해 파일의 내용을 읽어보면 위치상으로 13자리 이동된 비밀번호를 확인할  수 있다.

참고로, 위치를 이동하여 암호화한 방식을 '시저암호' 라고 한다.

![bandit11_3](/public/img/bandit11_3.PNG) 

<br/>

이동된 위치를 재배치 하기위해 tr을 사용하자. tr(Translate)은 문자를 변경하거나 삭제한다.

A-N의 거리와 Z-M의 거리가 13이다. 즉, 위치가 13자리 이동한다면 A는 N으로 바뀌고 Z는 M으로 바뀐다.

```shell
cat ./data.txt | tr [A-Za-z] [N-ZA-Mn-za-m]
```

![bandit11_4](/public/img/bandit11_4.PNG) 

<br/>

다음 단계(Level 12)로 넘어가기 위한 비밀번호를 알 수 있다.

```shell
5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu
```




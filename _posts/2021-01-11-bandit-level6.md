---
layout: post
title: OverTheWire - Bandit (Level 6)
date: 2021-01-11 20:30:00 +0900
category: System_Hacking
---


# Bandit (Level 6)

#### 서버 어딘가에 있는 파일(소유자 bandit7, 소유그룹 bandit6, 크기 33 bytes)을 통해 다음 단계(Level 7)로 가는 비밀번호 알아내기

<br/>


> 접속해야 할 주소:  bandit.labs.overthewire.org
>
> 포트 번호: 2220
>
> 계정명: bandit6 
>
> 비밀번호: DXjZPULLxYr17uwoI01bNLQbtFemEgo7
>
> 필요한 명령어: ls, cd, cat, file, du, find, grep

<br/>

이전 단계(Level 5)에서 구한 비밀번호를 입력하여 로그인 한다.

```shell
ssh -p 2220 bandit6@bandit.labs.overthewire.org
```

<br/>

현재 디렉토리(홈 디렉토리)에는 별 다른 정보가 없다. 

![bandit6_1](/public/img/bandit6_1.PNG) 

<br/>

루트(/)디렉토리부터 해당 조건들을 만족하는 파일을 찾아보자. 

그런데 많은 오류 메세지들이 출력되어 파일을 찾기가 힘들기 때문에 /dev/null로 보내 처리한다.

```shell
find / -size 33c -user bandit7 -group bandit6 2> /dev/null
```

![bandit6_2](/public/img/bandit6_2.PNG) 

<br/>

cat 명령어를 통해 해당 파일을 읽어보자.

 ![bandit6_3](/public/img/bandit6_3.PNG) 

<br/>

다음 단계(Level 7)로 넘어가기 위한 비밀번호를 알 수 있다.

```shell
HKBPTKQnIay4Fw76bEy8PVxKEDQRKTzs
```


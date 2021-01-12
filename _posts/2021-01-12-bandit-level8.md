---
layout: post
title: OverTheWire - Bandit (Level 8)
date: 2021-01-12 14:00:00 +0900
category: System_Hacking
---


# Bandit (Level 8)

#### 'data.txt' 파일 속 단 한 번만 나타나는 다음 단계(Level 9)로 가는 비밀번호 알아내기

<br/>


> 접속해야 할 주소:  bandit.labs.overthewire.org
>
> 포트 번호: 2220
>
> 계정명: bandit8
>
> 비밀번호: cvX2JJa4CFALtqS87jk27qwqGhBM9plV
>
> 필요한 명령어: grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd

<br/>

이전 단계(Level 7)에서 구한 비밀번호를 입력하여 로그인 한다.

```shell
ssh -p 2220 bandit8@bandit.labs.overthewire.org
```

<br/>

ls 명령어를 통해 확인해보면 소유자는 bandit9, 소유그룹은 bandit8이고 크기가 약 33KB인 data.txt 파일을 찾을 수 있다. 또한, 소유자는 읽기와 쓰기 권한을 가지고 있으며 소유그룹은 읽기 권한만을 가지고 있다.

```shell
ls -al
```

![bandit8_1](/public/img/bandit8_1.PNG) 

<br/>

추가로 file 명령어를 통해 파일의 형식을 보면 ASCII text 파일임을 알 수 있다.

```shell
file ./data.txt
```

![bandit8_2](/public/img/bandit8_2.PNG)

<br/>

먼저, 파일을 읽기 쉽게 정렬해보자. 참고로 sort 명령어는 그 내용을 오름차순으로 정렬해준다.

```shell
cat ./data.txt | sort
```

![bandit8_3](/public/img/bandit8_3.PNG) 

<br/>

또한, 비밀번호는 단 한 번만 나온다고 했으므로 비밀번호를 제외한 다른 내용들은 중복된 값이라고 추측할 수 있다. 

uniq 명령어를 통해 연속으로 중복되는 값들을 제거 후, -c 옵션을 통해 중복 횟수를 카운팅한 결과를 출력하면 그 횟수가 1인 값이 비밀번호다.

```shell
cat ./data.txt | sort | uniq -c
```

![bandit8_4](/public/img/bandit8_4.PNG) 

![bandit8_5](/public/img/bandit8_5.PNG) 

<br/>

다음 단계(Level 9)로 넘어가기 위한 비밀번호를 알 수 있다.

```shell
UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR
```




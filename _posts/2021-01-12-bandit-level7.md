---
layout: post
title: OverTheWire - Bandit (Level 7)
date: 2021-01-12 13:30:00 +0900
category: System_Hacking
---


# Bandit (Level 7)

#### 'data.txt' 파일 속 'millionth' 단어 옆에 있는 다음 단계(Level 8)로 가는 비밀번호 알아내기

<br/>


> 접속해야 할 주소:  bandit.labs.overthewire.org
>
> 포트 번호: 2220
>
> 계정명: bandit7
>
> 비밀번호: HKBPTKQnIay4Fw76bEy8PVxKEDQRKTzs
>
> 필요한 명령어: grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd

<br/>

이전 단계(Level 6)에서 구한 비밀번호를 입력하여 로그인 한다.

```shell
ssh -p 2220 bandit7@bandit.labs.overthewire.org
```

<br/>

ls 명령어를 통해 확인해보면 소유자는 bandit8, 소유그룹은 bandit7이고 크기가 약 4000 KB인 data.txt 파일을 찾을 수 있다. 또한, 소유자는 읽기와 쓰기 권한을 가지고 있으며 소유그룹은 읽기 권한만을 가지고 있다.

```shell
ls -al
```

![bandit7_1](/public/img/bandit7_1.PNG) 

<br/>

추가로 file 명령어를 통해 파일의 형식을 보면 UTF-8 Unicode text 파일임을 알 수 있다.

```shell
file ./data.txt
```

![bandit7_2](/public/img/bandit7_2.PNG)

<br/> 파일의 크기가 크기 때문에 cat 명령어로 모든 파일의 내용을 보고 찾기는 힘들다. 

비밀번호는 'millionth' 단어 옆에 있다고 했으므로, grep 명령어를 통해 직접 특정 단어를 포함한 행을 출력한다. 

```shell
cat ./data.txt | grep millionth
```

![bandit7_3](/public/img/bandit7_3.PNG) 

<br/>

다음 단계(Level 8)로 넘어가기 위한 비밀번호를 알 수 있다.

```shell
cvX2JJa4CFALtqS87jk27qwqGhBM9plV
```




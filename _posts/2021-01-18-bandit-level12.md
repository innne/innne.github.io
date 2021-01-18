---
layout: post
title: OverTheWire - Bandit (Level 12)
date: 2021-01-18 23:00:00 +0900
category: System_Hacking
---


# Bandit (Level 12)

#### 'data.txt' 파일은 반복적으로 압축된 16진수 덤프 파일이다. '/tmp' 디렉토리에서 mkdir 명령어를 이용하여 다음 단계(Level 13)로 가는 비밀번호 알아내기

<br/>


> 접속해야 할 주소:  bandit.labs.overthewire.org
>
> 포트 번호: 2220
>
> 계정명: bandit12
>
> 비밀번호: 5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu
>
> 필요한 명령어: grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd, mkdir, cp, mv, file

<br/>

이전 단계(Level 11)에서 구한 비밀번호를 입력하여 로그인 한다.

```shell
ssh -p 2220 bandit12@bandit.labs.overthewire.org
```

<br/>

ls 명령어를 통해 data.txt 파일을 찾을 수 있다. 

```shell
ls -al
```

![bandit12_1](/public/img/bandit11_1.PNG) 

<br/>

추가로 file 명령어를 통해 파일의 형식을 보면 ASCII text 파일이다.

```shell
file ./data.txt
```

![bandit12_2](/public/img/bandit12_2.PNG)

<br/>

cat 명령어를 통해 파일의 내용을 읽어보면 덤프 파일인 것을 확인할 수 있다.

![bandit12_3](/public/img/bandit12_3.PNG) 

<br/>

현재 디렉토리에서 우리는 소유자, 소유그룹에 속하지 않는 others이고, 쓰기 권한이 없기 때문에 덤프 파일을 복원시켜 새로운 파일을 생성시킬 수 없다. 그러므로 /tmp 디렉토리에서 mkdir 명령어를 이용해 우리의 디렉토리를 생성한 후, data.txt 파일을 copy 하여 가져온다.

```shell
mkdir /tmp/mytmp
cp ./data.txt /tmp/mytmp
cd /tmp/mytmp
ls -al
```

![bandit12_4](/public/img/bandit12_4.PNG) 

<br/>

이제 xxd 명령어를 이용해 덤프 파일을 mypw 파일에 복원시키자.

mypw 파일 형식을 확인해보면 gzip 파일임을 알 수 있다.

```shell
xxd -r ./data.txt > ./mypw
file ./mypw
```

![bandit12_5](/public/img/bandit12_5.PNG) 

<br/>

gzip을 통해 mypw 파일의 압축을 풀어보자. 하지만 확장자를 제대로 써주지 않으면 오류가 나므로 mv 명령어를 이용해 'mypw.gz'로 파일 이름을 변경해주자.

```shell
mv ./mypw ./mypw.gz
gzip -d ./mypw.gz
```

![bandit12_6](/public/img/bandit12_6.PNG) 

<br/>

gzip 으로 압축을 푼 mypw 파일의 형식을 다시 확인하니 bzip2로 압축되어 있다고 한다. bzip2 압축을 풀자 mypw.out 파일을 사용하라고 한다.

mypw.out 파일을 보니 다시 gzip으로 압축되어 있다고 하므로 풀어주자.

```shell
bzip2 -d ./mypw
file ./mypw.out
mv ./mypw.out ./mypw.out.gz
gzip -d ./mypw.out.gz
```

<br>

압축을 푼 결과 mypw.out 파일은 archive 형식이다.

![bandit12_7](/public/img/bandit12_7.PNG) 

<br/>

tar를 통해 archive 파일을 풀어주었다. 그러자 data5.bin이라는 파일이 생성된 것을 볼 수 있다. 

```shell
tar -xvf ./mypw.out
```

![bandit12_8](/public/img/bandit12_8.PNG) 

<br/>

그 후 다양한 형식의 파일들을 계속 생성되고 우리는 이전 방식처럼 계속해서 압축을 풀어주어야 한다. 마지막으로 생성된 data8.bin 파일 형식을 보니 드디어 ASCII text 파일이다.

cat 명령어를 통해 비밀번호를 확인하자.

```shell
file ./data5.bin
tar -xvf ./data5.bin
file ./data6.bin
bzip -d ./data6.bin.out
file ./data8.bin
mv ./data8.bin ./data8.bin.gz
file ./data8.bin
cat ./data8.bin
```

![bandit12_9](/public/img/bandit12_9.PNG) 

<br/>

다음 단계(Level 13)로 넘어가기 위한 비밀번호를 알 수 있다.

```shell
8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL
```




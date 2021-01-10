---
layout: post
title: WebGoat - SQL Injection (advanced 2)
date: 2021-01-10 23:00:00 +0900
category: Web_Hacking
---

# WebGoat - SQL Injection (advanced 2)

#### 'tom' 계정으로 로그인하기

<br/>

> Blind SQL Injection 이란 SQL 쿼리의 참/거짓 결과를 통해 데이터베이스 정보를 파악하는 공격  

<br/>

기존에 사용했던 방법으로는 LOGIN이 되지 않아 REGISTER에서 방법을 찾아보기 위해 'test' 계정을 생성하였다.

![webgoat_sqli_adv2_1](/public/img/webgoat_sqli_adv2_1.PNG)

<br/>

같은 ID를 생성하려고 하니 이미 존재하는 계정이기 때문에 생성할 수 없다고 한다. 이는 REGISTER 과정에 SELECT문이 숨어있다는 것을 의미하므로 SQL Injection을 시도해보았지만 통하지 않는다.

![webgoat_sqli_adv2_3](/public/img/webgoat_sqli_adv2_3.PNG)

<br/>

Blind SQL Injection을 시도해보니 참/거짓 조건에 따라 결과가 달라지는 것을 알 수 있다.

![webgoat_sqli_adv2_4](/public/img/webgoat_sqli_adv2_4.PNG)

![webgoat_sqli_adv2_5](/public/img/webgoat_sqli_adv2_5.PNG)

<br/>

또한, 해당 테이블에 'userid', 'password' 라는 애트리뷰트가 있고, tom의 비밀번호는 23자리라는 것을 확인할 수 있다.

![webgoat_sqli_adv2_6](/public/img/webgoat_sqli_adv2_6.PNG)

![webgoat_sqli_adv2_7](/public/img/webgoat_sqli_adv2_7.PNG)

![webgoat_sqli_adv2_8](/public/img/webgoat_sqli_adv2_8.PNG)

<br/>

하지만 아래와 같은 방법으로 23자리의 비밀번호에 대해 각각 'a'부터 'z'까지 비교하며 알아내는 것은 오랜 시간이 걸린다. 하여 Burp Suite의 자동화 툴을 이용하였고 최종적으로 찾은 비밀번호는 'thisisasecretfortomonly' 이다.

![webgoat_sqli_adv2_9](/public/img/webgoat_sqli_adv2_9.PNG)

<br/>

LOGIN에서 'tom'과 'thisisasecretfortomonly'를 입력하니 성공이다.

![webgoat_sqli_adv2_10](/public/img/webgoat_sqli_adv2_10.PNG)


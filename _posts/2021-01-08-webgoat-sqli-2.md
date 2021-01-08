---
layout: post
title: WebGoat - SQL Injection (2)
date: 2021-01-08 18:30:00 +0900
category: Web_Hacking
---

# WebGoat - SQL Injection (2)

#### 입력 폼을 활용하여 "users" 테이블에서 모든 사용자 검색하기

<br/>

> SQL Injection 이란 악의적인 SQL 쿼리를 삽입하여 데이터베이스 조회, 삭제, 변조하는 공격이다. 

<br/>

아래의 쿼리는 단순히 숫자 값을 연결하여 동적 쿼리를 구성하므로 Numeric SQL Injection에 취약하다.

```shell
"select * from users where USERID = "  + userID;
```

<br/>

아래의 입력 폼을 활용하여 "users" 테이블에서 모든 사용자를 검색하라. 전체 사용자 리스트를 얻기 위해서 특정 사용자의 이름을 알 필요는 없다. 그러나 '101'을 사용하면 한 사용자의 데이터를 검색할 수 있다.

![webgoat_sqli2_1](/public/img/webgoat_sqli2_1.PNG)

<br/>

입력 폼에 101을 입력하면 결과는 다음과 같다.

![webgoat_sqli2_2](/public/img/webgoat_sqli2_2.PNG)

<br/>

모든 사용자를 검색하기 위해 101 or 1=1 을 입력하면 or 조건을 통해 결과가 항상 참이 되므로 모든 레코드가 출력된다.

![webgoat_sqli2_3](/public/img/webgoat_sqli2_3.PNG)


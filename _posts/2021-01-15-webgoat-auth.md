---
layout: post
title: WebGoat - Authentication Bypass
date: 2021-01-15 16:00:00 +0900
category: Web_Hacking
---

# WebGoat - Authentication Bypass

#### 비밀번호 재설정 중 가입 시 설정한 보안 질문들에 답하여 본인 계정임을 증명하기

<br/>

> Authentication Bypass(인증우회)란 설정이나 논리상의 결함을 이용해 데이터를 변조하여 요구 조건을 만족시키는 것을 말한다.

<br/>'test'라고 입력한 후 Burp Suite를 통해 보면 POST 방식으로 각각 'secQuestion0', 'secQuestion1' 파라미터를 통해 데이터가 전달된다는 것을 알 수 있다.

![webgoat_auth_1](/public/img/webgoat_auth_1.PNG)

![webgoat_auth_2](/public/img/webgoat_auth_2.PNG)

<br/>

이제 request를 intercept하여 body부분을 다음과 같이 수정하여 전송해보자.

```shell
secQuestion123=test&secQuestion456=test&jsEnabled=1&verifyMethod=SEC_QUESTIONS&userId=12309746
```

![webgoat_auth_3](/public/img/webgoat_auth_3.PNG)

<br/>

그 결과, 비밀번호 재설정 화면이 나오면서 인증우회에 성공하였다.

즉 'secQuestion0', 'secQuestion1'의 번호를 변경하면 인증을 우회하는 결함을 확인할 수 있었다.

![webgoat_auth_4](/public/img/webgoat_auth_4.PNG)


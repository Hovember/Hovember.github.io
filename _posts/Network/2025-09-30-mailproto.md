---
title: "메일 프로토콜 (SMTP, POP3, IMAP)"
excerpt: "메일 프로토콜을 알아보자"
categories:
  - Network
date: 2025-09-30
last_modified_at: 2025-09-30
---
<br>
이해하기 쉽게 그림을 넣을 생각입니다.

## SMTP(Simple Mail Transfer Protocol)

이메일을 전송할 때 사용하는 프로토콜이다. 

이 프로토콜이 사용되는 경우는 두 가지로<br>
1. 클라이언트에서 메일 서버로 전송할 때<br>
2. 서버 간 메일을 전송할 때

sender@gmail.com 이 메일을 보내는 사람<br>
receiver@naver.com 이 메일을 받는 사람으로 해서 예를 들어보겠다.

1. sender@gmail.com(클라이언트)가 smtp.gmail.com (smtp 서버)로 메일 전송 <br>
2. smtp 서버는 수신자의 주소(receiver@naver.com)를 확인 @naver.com 도메일을 가진 메일이므로 naver로 메일 전달해야겠다고 판단<br>
3. gmail smtp 서버는 dns에서 naver.com의 mx 레코드 조회 그리고나서 dns에서 mx.naver.com의 ip주소를 알아낸다<br>
4. gmail smtp 서버가 naver 메일 서버에 smtp 프로토콜로 접속해서 메일 전달

SMTP 프로토콜로 접속해서 메일을 전달한다는 것은 TCP 소켓을 열어(25번 포트로 TCP 연결을 연다) SMTP 명령어와 응답을 주고 받는 것이다.

따라서 1번과 4번의 경우가 SMTP 프로토콜이 사용되는 경우이다. 

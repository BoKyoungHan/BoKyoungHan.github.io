---
layout: post
title: "[Linux] 환경변수 확인하기"
categories: [Linux]
tags: [linux, command]
---

## Intro
리눅스에서 환경변수 목록을 확인하는 방법에 대한 글이다.

<br><br>

## 환경변수 확인 명령어: export
> $ export

터미널에 **export** 명령어를 입력하면 아래와 같이 시스템의 환경변수 목록이 뜬다.

![image](/assets/img/posts/200923_1.jpg)

**export** 명령어를 사용하면 시스템의 환경변수 목록 전체가 떠서 확인하고자 하는 환경변수의 값을 찾기 어려울 수 있다.
이럴 때 **echo** 명령어를 사용하면 특정 환경변수의 값만 확인할 수 있다.

> $ echo $[환경변수]

![image](/assets/img/posts/200923_2.jpg)




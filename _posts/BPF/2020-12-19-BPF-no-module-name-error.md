---
layout: post
title: "[BPF] No module named bcc 에러"
categories: [BPF, Troubleshooting]
tags: [troubleshooting, bpf]
---

### Intro
---
잘 되던 bpf program 이 No module named bcc 이라는 에러를 출력하며 실행되지 않음..

<br><br>
### Troubleshooting
---
`python version`이 `3.6`이여서 발생한 문제이다.
_(구글링 열심히 하고 커널 컴파일 했는데 그 시간의 일부가 매몰비용으로 바뀌는 순간,, 좋으면서 싫다. 사실 예전에도 이 문제 겪었다 해결했는데 정리해놓지 않아 까먹어서 같은 문제를 또 겪었다. 이번에는 정리해야지!)_
<br>bpf 프로그래밍 할 때 `python version`이 `2.7`이 되어야 하는 것 같다.

그래서 파이썬 버전 바꾸는 방법도 함께 메모.
아래 내용은 파이썬 3.6을 2.7 버전으로 바꾸는 내용을 담고 있다.

<br>

**1) 현재 파이썬 버전 확인**
```console
$ ls /usr/bin/ | grep python
```

**2) 파이썬 버전 등록 및 변경**
<br>파이썬 버전을 변경하는 옵션이다.
<br>만약 아래 error 로그처럼 설정된 것이 없다면 아무것도 등록된 것이 없다는 의미이다.

```console
$ sudo update-alternatives --config python
update-alternatives: error: no alternatives for python
```

`update-alternatives --install [symbolic link path] python [real path] number` 명령어는 실행파일을 등록하는 명령어이다.

아래와 같이 입력하면 2.7 버전이 update-alternatives에 등록된다. 물론 파이썬 2.7이 설치되어 있어야 한다.

```console
$ sudo update-alternatives --install /usr/bin/python python /usr/bin/python2.7 1
```

<br>
`update-alternatives --config python` 을 다시 입력하면 등록한 파이썬 버전을 선택하는 메뉴가 나온다.

```console
$ sudo update-alternatives --config python
```
![img](/assets/img/posts/201219_1.png)

원하는 메뉴의 번호를 입력하고 파이썬 버전을 확인해 보자.
<br>나의 경우 1을 선택했다.

**3) 파이썬 버전 확인**

```console
$ python --version
python 2.7.17
```

<br><br><br>
reference: [1](https://codechacha.com/ko/change-python-version/)



---
layout: post
title: "[Linux] 외부 통신 오류"
categories: [Linux, Troubleshooting]
tags: [linux]
---

## Intro
리눅스 서버를 재부팅 할 일이 생겼다.
재부팅 후에 git repository를 clone해서 가져오려고 시도하였는데 다음과 같은 오류가 발생했다.

```console
bkhan@jsshim-desktop:~$ git clone https://github.com/ithemal/bhive.git
Cloning into 'bhive'...
fatal: unable to access 'https://github.com/ithemal/bhive.git/': Could not resolve host: github.com
```

구글에 오류 메시지 **Could not resolve host: github.com** 를 검색하니 아래와 같은 커맨드가 해결 방안이 될 수 있다고 하여 시도해 보았으나 여전히 동작하지 않았다.

```console
$ git config --global --unset http.proxy
$ git config --global --unset https.proxy
```

그러다 문제를 해결하는 방법을 찾아냈고, 이에 대해 정리해보기로 하였다.

<br><br>
## Troubleshooting
#### ✔️ 네트워크 외부 통신 상태 확인

우선 `ping` 으로 외부 통신이 가능한지 확인한다.

```console
bkhan@jsshim-desktop:~$ ping 8.8.8.8
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=113 time=45.7 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=113 time=45.8 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=113 time=48.7 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=113 time=45.5 ms
```

위와 같은 메시지가 뜨면 네트워크 외부 통신이 가능한 것이다.

#### ✔️ 도메인 확인
네트워크 준비가 완료된 것을 확인한 후 도메인을 통한 통신을 시도해 보았다.

```console
bkhan@jsshim-desktop:~$ ping www.google.com
ping: www.google.com: Name or service not known
```

에러가 뜨는 것을 확인. 
이유는 **도메인 명을 IP로 매칭해주는 설정**이 세팅되어 있지 않아서 그렇다.
즉, 도메인 명을 IP로 변환해주는 **DNS 서버를 등록**해 주어야 한다.

(내가 이용하고 있는 서버의 경우 재부팅 때마다 수동으로 설정해주어야 하는 것 같다.)

#### ✔️ DNS 서버 추가
DNS 서버를 추가해주자. 참고한 블로그에서는 KT의 공인된 수퍼 DNS 서버를 이용하였고, 나도 동일한 DNS 서버를 사용하였다.

편집기로 `/etc/resolv.conf` 파일을 열어 `nameserver 168.126.63.1` 을 추가해준다.
이 작업은 문자열을 입력할 시 168.126.63.1 서버에 저장된 DNS ZONE 정보의 내용을 참조하겠다는 것을 의미한다.

```python
nameserver 127.0.0.53
nameserver 168.126.63.1
options edns0
```

추가 작업이 끝난 후 파일을 저장하고 다시 `ping www.google.com` 명령어를 실행시켜 정상적으로 작동하는지 확인을 해보았다.

#### ✔️ 결과 확인

```console
bkhan@jsshim-desktop:~$ ping www.google.com
PING www.google.com (172.217.25.228) 56(84) bytes of data.
64 bytes from nrt12s14-in-f4.1e100.net (172.217.25.228): icmp_seq=1 ttl=114 time=36.7 ms
64 bytes from nrt12s14-in-f4.1e100.net (172.217.25.228): icmp_seq=2 ttl=114 time=38.1 ms
```

정상적으로 작동하는 것을 확인할 수 있었다.

마지막으로 하고자 했던 git clone 명령어를 다시 시도해 보았다.

```console
bkhan@jsshim-desktop:~$ **git clone https://github.com/ithemal/bhive.git**
Cloning into 'bhive'...
remote: Enumerating objects: 65, done.
remote: Counting objects: 100% (65/65), done.
remote: Compressing objects: 100% (58/58), done.
remote: Total 234 (delta 20), reused 27 (delta 7), pack-reused 169
Receiving objects: 100% (234/234), 30.03 MiB | 9.42 MiB/s, done.
Resolving deltas: 100% (134/134), done.
```

`git clone`에 성공했다.

<br><br><br><br><br>

references: [1](https://myungin.tistory.com/entry/02-%EB%A6%AC%EB%88%85%EC%8A%A4%EB%A5%BC-%EC%84%A4%EC%B9%98%ED%96%88%EB%8A%94%EB%8D%B0-%EC%99%B8%EB%B6%80-%ED%86%B5%EC%8B%A0%EC%9D%B4-%EC%95%88%EB%90%98%EC%9A%94)

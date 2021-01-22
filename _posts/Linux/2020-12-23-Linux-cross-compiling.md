---
layout: post
title: "[Linux] Cross Compiling"
categories: [Linux]
tags: [linux]
---


## Intro
---
McPat 라는 프로그램을 컴파일해야 하는 상황.

makefile 이 .mk 확장자의 파일을 호출하는 형식이었다.

찾아보니 트리 형식의 makefile 구조였다.

```console
.mk 확장자
mk 확장자는 Makefile을 최상위에 두고 그 하위에 두는 참조되는 다른 makefile 즉, 다른 makefile 확장자이다.
```

## Problem
---

```console
$ make
```

`make` 커맨드를 입력하니 아래 오류가 발생함. <br>

```console
bkhan@osproject:~/mcpat$ make
mkdir obj_opt
make[1]: Entering directory '/home/bkhan/mcpat'
g++ -m32 -Wno-unknown-pragmas -O3 -msse2 -mfpmath=sse -DNTHREADS=4 -Icacti -c cacti/Ucache.cc -o obj_opt/Ucache.o
In file included from /usr/include/time.h:25,
from cacti/Ucache.cc:33:
/usr/include/features.h:461:12: fatal error: sys/cdefs.h: No such file or directory
461 | # include <sys/cdefs.h>
| ^
compilation terminated.
make[1]: [mcpat.mk:77: obj_opt/Ucache.o] Error 1
make[1]: Leaving directory '/home/bkhan/mcpat'
make: [makefile:11: opt] Error 2
```
원인은 64-bit 환경에서 32-bit 프로그램을 컴파일 하려고 했기 때문.
환경은 우분투 20.04 64-bit


## Solution
---

```console
$ sudo apt-get install libx32gcc-4.8-dev
$ sudo apt-get install libc6-dev-i386
```

여기까지 설치했을 때 첫 번째 에러가 해결됨

`.mk` 파일 내의 컴파일 옵션에 아래 옵션 추가.

```c
-m64
```
최종적으로 컴파일이 되면서 바이너리파일이 생성된 것을 확인!

<br><br>
references: [1](https://m.blog.naver.com/PostView.nhn?blogId=5boon&logNo=220508654072&proxyReferer=https:%2F%2Fwww.google.com%2F), [2](https://stackoverflow.com/questions/4643197/missing-include-bits-cconfig-h-when-cross-compiling-64-bit-program-on-32-bit)

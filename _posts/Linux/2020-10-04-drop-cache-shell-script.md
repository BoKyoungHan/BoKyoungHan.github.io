---
layout: post
title: "[Linux] drop cache shell script"
categories: [Linux]
tags: [linux]
---

## Intro
---
리눅스에서 캐시 메모리를 비울 때 사용하는 쉘 스크립트이다.

<br><br>

## Script
### 쉘 스크립트 작성하기

```console
$ vim drop_cache.sh
```
vim으로 임의의 파일을 하나 만든 후 아래의 내용을 추가한다.

```shell
#!/bin/bash

sync
echo 1 > /proc/sys/vm/drop_caches
```
캐시를 계속 비워줘야 하는 상황이라면 while문을 추가하여 아래와 같이 작성하면 된다.

```shell
#!/bin/bash

while :
do
    sync
    echo 1 > /proc/sys/vm/drop_caches
done
```

<br>

### 쉘 스크립트 실행시키기
참고로 해당 스크립트를 실행하기 위해선 root 권한이 필요하다.

```console
$ sudo sh drop_cache.sh
```


<br>

### 결과 확인하기
dmesg 명령어 (커널 메시지 확인) 를 통해 수행 여부를 확인할 수 있다.

```console
$ dmesg
```

성공적으로 실행 시 아래와 같은 메시지가 출력된다.
(while문으로 캐시를 계속 비워줬을 때라 drop_caches 메시지가 연속적으로 출력된 것을 확인할 수 있다.)

![img](/assets/img/posts/201004_1.png)

---
layout: post
title: "[Ubuntu] silversearcher-ag"
categories: [Ubuntu]
tags: [ubuntu]
---

## Intro
소스 코드들이 담긴 폴더 내에서 특정 문자열을 찾을 때 흔히 `grep`을 많이 사용한다.
<br>이번에는 `grep`과 유사하지만 검색 결과를 `grep`과는 다른 방식으로 나타내주는 `sileversearcher-ag`를 소개해본다. 

<br><br>

## Intall
```console
$ sudo apt-get install silversearcher-ag
```
<br><br>

## How to use
```console
$ ag [target_string]
```

결과는 아래 그림과 같다.
<br>우선 타겟 문자열을 담은 파일의 위치가 표시되고 문자열이 위치한 라인이 라인 번호와 하이라이트 된 문자열과 함께 보여진다.

![img](/assets/img/posts/200923_3.png)

개인적으로 `grep`과 비교했을 때 파일 별로 결과를 보여준다는 점에서 가독성이 있는 것 같다.

```console
$ ag --help 
```
위 명령어를 통해 더 많은 옵션을 확인할 수 있으니 용도에 따라 사용하면 될 것 같다.

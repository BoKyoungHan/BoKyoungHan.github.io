---
layout: post
title: "[Linux] 오류 메시지 출력 함수: perror()"
categories: [Linux]
tags: [linux, cpp]
---

## Intro
리눅스에는 시스템콜 및 라이브러리 함수를 수행하다가 오류가 발생하면 사용자의 프로그램으로 오류 결과를 넘겨준다.
이번 포스팅에서는 오류 메시지를 출력하고자 할 때 사용할 수 있는 함수에 대해 정리해 보고자 한다.

참고) 일반적으로 오류 발생 시 리턴값은 다음과 같다.
시스템 콜 오류 시: -1
라이브러리 함수 오류 시: NULL

<br><br>
## 오류 메시지 출력 함수: perror()
### ✔️ perror()
오류 메시지를 출력할 때 많이 사용하는 함수 `perror()`의 형식은 다음과 같다.

```c
#include <stdio.h>
void perror(const char *s);
```

이때 매개변수 s에는 오류 메시지 앞에 덧붙이고 싶은 문자열을 전달하면 된다.

### ✔️ 사용 예제
```c
int main(void)
{
    int fd;
	fd = open("anyfile", O_RDONLY);
	if (fd == -1){
	    perror("open");
		exit(1);
	}
	return 0;
}
```

위 코드를 실행시켰을 때, **open()** 함수에서 오류가 발생할 경우 **perror()** 함수에서 발생한 오류 메시지를 출력하게 된다.

만일 오류가 발생했을 경우 출력 메시지는 다음과 같다.

```console
open: No such file or directory
```
`perror(**open**)`; 과 같이 `open` 을 인자로 건네주었기 때문에 오류 메시지 앞에 해당 문자열이 출력되는 것을 확인할 수 있다.

알고 쓰면 유용할 것 같다!


<br><br><br><br><br>
references: [1](https://mintnlatte.tistory.com/288)

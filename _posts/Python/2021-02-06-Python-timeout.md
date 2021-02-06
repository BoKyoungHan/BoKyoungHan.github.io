---
layout: post
title: "[Python] subprocess 모듈 timeout 사용하기"
categories: [Python, Troubleshooting]
tags: [python, troubleshooting]

---



## Intro

python에서 subprocess 모듈을 사용하여 외부 프로그램을 실행시켰을 때, <br>외부 프로그램에서 오류가 발생하여 무한 대기를 해야 하는 상황이 발생할 수 있다.

이 경우 상위 프로세스인 python에서 적절하게 외부 프로그램을 종료시켜 줄 필요가 있으며, 해당 기능은 subprocess 모듈의 timeout 기능을 통해 사용 가능하다.

이번 포스팅은 python의 subprocess 모듈에서 timeout을 어떻게 사용하는지에 대해 다루고 있다.

> _참고로 timeout 기능은 python version 3.3 이상에서만 사용 가능하다고 하니<br> `$ python --verion` 명령어를 통해 현재 python 버전을 확인하도록 하자.<br>만일 버전이 3.3 보다 낮을 경우 적당한 버전을 새로 설치하거나 기존에 설치되어 있는 버전 목록을 확인하여 버전을 변경해주면 된다.<br>버전을 변경하는 방법은 [링크](https://bokyounghan.github.io/posts/BPF-no-module-name-error/) 를 통해 확인할 수 있다._

<br><br>

## _subprocess_ 모듈을 사용하여 외부 프로그램 실행시키기

`timeout` 을 사용하기 전 우선 `subprocess`를 사용하는 방법에 대해 간단히 다루고 넘어가려고 한다.

`subprocess`를 사용하는 방법은 다음과 같다.

```python
import subprocess

test = subprocess.Popen(['./harness-source/test', BB,iteration],stdout=subprocess.PIPE)
```

간단하게 설명하자면, `subprocess`를 `import`한 뒤<br>호출하고자 하는 외부 프로그램명과 해당 외부프로그램에 필요한 인자 2개를 Popen에다 차례로 입력하면 된다.

나는 위 예제에서 `./harness-source/test` 라는 바이너리 파일을 `BB` 와 `iteration` 을 인자로 주어 실행시켰다. <br>_(참고로 BB와 iteration 인자는 예제에는 정의되어 있지 않지만 프로그램에서 따로 구하는 값들이다.)_



<br><br>



## 외부 프로그램의 실행 결과 가져오기

위에서는 `subprocess`모듈을 통해 외부 프로그램을 어떻게 실행시키는지에 대해 다루었다.

외부 프로그램을 실행시키다 보면 실행 결과를 받아와 2차 가공이 필요한 경우가 발생할 수 있다.<br>그럴 경우 다음과 같은 명령어를 사용하면 된다.

```python
out, err = test.communicate()
```



<br><br>

## _timeout_ 인자 사용하기

포스팅의 목적인 `timeout`인자는 다음과 같이 사용한다.

```python
try:
    out, err = test.communicate(timeout = 5)

except:
    test.kill()
```

본 예제에서는 5초 뒤에 외부 프로그램이 응답하지 않으면 예외 구문을 이용하여 외부 프로그램을 종료시키도록 설정하였다.

프로그램이 적절하게 종료되는 타이밍을 계산하여 timeout 시간을 설정하면 될 것 같다.



<br><br><br>

reference: [1](http://blog.naver.com/PostView.nhn?blogId=wwwkasa&logNo=220952303071)



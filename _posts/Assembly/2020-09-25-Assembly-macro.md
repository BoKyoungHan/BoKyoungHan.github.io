---
layout: post
title: "[Assembly] 매크로 사용하기"
categories: [Assembly]
tags: [assembly]
---

## 매크로
어셈블리에서 매크로는 타 프로그래밍 언어에서 사용하는 매크로와 의미가 같다.
<br>어셈블리 언어의 코드 블럭에 이름을 붙여 필요할 때마다 불러서 사용하는 개념이다.

### ✔️ 매크로 정의하기
매크로의 시작과 끝에 **%macro**, **%endmacro** 선언
<br>**매크로 이름**과 **매개변수** 선언

### ✔️ 사용 예시
```c
%macro CLEARXMMREG 1 ; clear one xmm register
xor xmm%1, xmm%1
%endmacro
```

위 매크로를 간단하게 설명하자면, `xor` 연산을 이용해서 `xmm(MultiMedia eXtensions)` 레지스터를 초기화 시키는 매크로이다.


매크로 이름 **CLEARXMMREG** 뒤에 정의한 매개변수 **1**은 한 개의 매개변수를 사용하겠다는 것을 의미한다.
<br>컴파일러는 컴파일 시에 **%1** 자리에 **입력한 매개변수 값**을 넣어 코드를 재구성한다.

위에서 정의한 매크로는 다음과 같이 사용할 수 있다.

```c
CLEARXMMREG 2
```

이 경우 매크로 내용에 매개변수 2가 들어가며 코드는 아래와 같이 구성된다.

```c
xor xmm2, xmm2
```

### ✔️ 더 많은 매개변수를 가지는 매크로
매크로는 더 많은 수의 매개변수를 가질 수 있다.
<br>두 개의 매개변수를 가지는 매크로를 예로 들어보고자 한다.

```c
%macro read_perf_counter 2
mov rcx, %1
rdpmc
combine_rax_rdx(%2)
%endmacro
```

매크로 이름 `read_perf_counter`과 사용할 매개변수 개수 `2` 를 정의하였다. 
<br>매개변수를 입력하면 입력한 순서대로 `%1`, `%2`이 해당 값으로 대체된다.

사용 예제이다.

```c
read_perf_counter counter_core_cyc, r12
```

두 개의 매개변수 `counter_core_cyc`, `r12` 를 입력했다.
<br>컴파일 시 컴파일러가 `%1`을 `counter_core_cye`로, `%2`를 `r12`로 치환할 것이다.

```c
mov rcx, counter_core_cyc
rdpmc
combine_rax_rdx(**r12**)
```

 <br><br>
 _어셈블리 코드를 보는 게 생각보다 어렵다. 문법 하나하나 알아가다 보면 언젠간 c코드처럼 읽을 수 있겠지ㅠ!_


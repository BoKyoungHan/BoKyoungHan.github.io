---
layout: post
title: "[Operating Systems] Priority Inversion"
categories: [OperatingSystems]
tags: [os]
---

## Intro
Lottery Scheduling과 관련된 논문을 읽는데 priority inversion 개념이 나왔다.
분명 배운 개념인데, 바로 떠오르지 않아서 검색을 해봤다. 찾아본 김에 정리해둔다.

<br><br>

## Priority Inversion
### ✔️ 정의
Priority Inversion이란 사전적 의미로 **높은 우선순위의 프로세스가 낮은 우선순위의 프로세스로 인하여 수행이 block 되어 있는 상태**를 말한다.

### ✔️ 언제 발생하는가?
주로 공유 자원의 동기화로 인하여 발생한다.

예를 들어, 우선순위가 높은 프로세스 P1과 낮은 P2가 있고 두 프로세스가 critical section을 공유하고 있다고 가정하자.

P2가 critical section에 들어가 수행을 시작하고, 뒤이어 P1이 critical section에서 수행할 일이 생겼다.
이 상황에서 P1은 P2보다 우선순위가 더 높음에도 불구하고, P2의 critical section에서의 수행이 끝나기를 기다려야 한다.

이처럼 높은 우선순위를 가진 P1이 낮은 우선순위를 가진 P2의 수행을 기다려야 하는 상황을 통틀어 priority inversion이라고 칭한다.

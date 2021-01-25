---
layout: post
title: "[Computer Architecture] ISA(Instruction Set Architecture)"
categories: [ComputerArchitecture]
tags: [computerarchitecture]
---

## Intro
대학원 입시 공부를 할 때 컴퓨터 구조를 처음부터 다시 공부했었다. _(지진 컴구의 여파라고 해둔다..)_
<br>이번 포스팅에서는 그때 추상적으로 다가왔던 ISA에 대한 개념을 좀 더 구체화 시켜보려고 한다.


<br><br>

## ISA (Instruction Set Architecture)
ISA는 글자 그대로 해석하자면 명령어 집합 구조이며, 하드웨어와 소프트웨어 간의 커뮤니케이션을 가능하게 하는 인터페이스라고 할 수 있겠다.

보다 자세한 이해를 위해 아래 그림을 살펴보자.
<br>아래 그림은 컴퓨터 시스템을 레이어별로 추상화하여 나타낸 것이다. 
<br>가장 상위 레이어인 어플리케이션 레이어부터 시작하여 다양한 레이어를 거쳐 SW 레이어에서 HW 레이어로 레이어 단계가 넘어가게 되는데, 이때 **SW에서 HW로 넘어가는 단계**에 위치하면서 이들간의 **중재자** 역할을 해주는 것이 바로 ISA이다.

따라서 ISA는 최하위 레벨의 프로그래밍 인터페이스로 정의될 수 있으며, 프로세서가 실행할 수 있는 모든 명령어들을 포함하고 있다.

![img](/assets/img/posts/200910_1.png)

<br><br>

## ADT (Abstract Data Type)
ISA를 Abstract Data Type (ADT) 개념을 통해 나타낼 것인데, 그 전에 ADT가 무엇인지 정의해보려고 한다.

### ADT란
> _**A set of data values (state) and associated operations** that are precisely specified independent of any particular implementation_

ADT, 즉 추상 자료형이란 **자료**와 **그 자료를 이용한 연산들의 집합**을 의미한다.
자료구조 Stack을 예로 들어보면, Stack의 원소는 자료에 해당하고, push()와 pop()등의 연산은 자료를 이용한 연산들에 해당한다. 

덧붙여 말하자면, 추상 자료형은 구체적 구현 방법을 명시하지 않는다는 특징을 가진다. 
<br>Stack을 사용할 때 원소의 타입과 push(), pop()과 같은 연산의 사용 방법을 알면 내부 구현 방법을 알지 못해도 해당 자료구조를 사용할 수 있는 걸 떠올려보자.

<br><br>

## ISA as an ADT
이제 ISA를 ADT 개념을 통해 나타내보자.

> _"...the attributes of a [computing] system as seen by the programmer, i.e. the conceptual structure (**state**) and functional behavior (**operations**), as distinct from the organization of the data flow and controls, the logical design, and the physical implementation."_  - Amdahl, Blaauw, and Brooks, 1994

_(컴퓨터구조를 배우기 시작했을 때 위 문장이 모호하게만 다가와 완전히 이해하기 힘들었다. 문장을 다시 읽어보니 보다 뚜렷하게 이해할 수 있어 왠지 모르게 감회가 새롭다.)_

<br>앞서 ADT를 '자료와 그 자료를 이용한 연산들의 집합' 이라고 정의하였는데, ISA에서 자료는 무엇이고 연산은 어떤 걸 의미할까?

<br>
아래 그림은 ISA를 ADT로 나타낸 것인데, 이해를 도울 수 있을 것 같다. 
그림을 살펴보자면 ISA에서 자료란 `Registers & Memory` 를 의미하며 연산이란 `Instruction`을 의미한다.
<br>`Instruction`이 수행되고 나면 레지스터의 값과 메모리 상태가 변하는 것을 떠올리면 이해가 수월할 거 같다.

![img](/assets/img/posts/200910_2.png) 
     
여기까지 왔을 때, ISA가 HW 레이어의 인터페이스라는 말에 동의를 할 수 있다면 좋겠다.

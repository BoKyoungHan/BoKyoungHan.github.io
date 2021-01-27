---
layout: post
title: "[Linux] 리눅스 CPU 동적으로 ON/OFF 시키기 (CPU Hotplug)"
categories: [Linux]
tags: [linux]
---

## Intro

리군스에서는 동적으로 CPU 코어를 켜고 끌 수 있는 Hotplug 기능을 제공한다.

이는 CPU 코어 개수에 따른 성능 테스트를 수행할 때 매우 유용하게 사용할 수 있는 기능이다.

_서버의 16개 코어 중 하나의 코를 통해 실험을 돌린 뒤 그 결과를 추출하기 위해 이 기능을 사용해 보려고 한다._ 



## 서버의 CPU 정보 확인하기

리눅스 서버의 CPU 정보는 `/proc/cpuinfo` 파일에서 확인할 수 있다.

콘솔에 다음과 같은 명령어를 입력하면 확인할 수 있다.

```console
$ cat /proc/cpuinfo
```



```console
processor       : 0
vendor_id       : GenuineIntel
cpu family      : 6
model           : 158
model name      : Intel(R) Core(TM) i9-9900K CPU @ 3.60GHz
stepping        : 13
microcode       : 0xde
cpu MHz         : 800.122
cache size      : 16384 KB
physical id     : 0
siblings        : 16
core id         : 0
cpu cores       : 8
apicid          : 0
initial apicid  : 0
fpu             : yes
fpu_exception   : yes
cpuid level     : 22
wp              : yes
flags           : fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush dts acpi mmx fxsr sse sse2 ss ht tm pbe syscall nx pdpe1gb rdtscp lm constant_tsc art arch_perfmon pebs bts rep_good nopl xtopology nonstop_tsc cpuid aperfmperf pni pclmulqdq dtes64 monitor ds_cpl vmx smx est tm2 ssse3 sdbg fma cx16 xtpr pdcm pcid sse4_1 sse4_2 x2apic movbe popcnt tsc_deadline_timer aes xsave avx f16c rdrand lahf_lm abm 3dnowprefetch cpuid_fault epb invpcid_single ssbd ibrs ibpb stibp ibrs_enhanced tpr_shadow vnmi flexpriority ept vpid ept_ad fsgsbase tsc_adjust bmi1 avx2 smep bmi2 erms invpcid mpx rdseed adx smap clflushopt intel_pt xsaveopt xsavec xgetbv1 xsaves dtherm ida arat pln pts hwp hwp_notify hwp_act_window hwp_epp md_clear flush_l1d arch_capabilities
bugs            : spectre_v1 spectre_v2 spec_store_bypass swapgs taa itlb_multihit srbds
bogomips        : 7200.00
clflush size    : 64
cache_alignment : 64
address sizes   : 39 bits physical, 48 bits virtual
power management:
```



위 정보를 해석하는 간단한 방법은 다음과 같다.

* processor: 논리적인 CPU의 ID
* physical id: 물리적인 CPU의 ID
* core id: 물리 CPU내에서 각 core에 할당되는 ID





## CPU ON/OFF 설정

CPU정보를 확인한 후, ON/OFF 시킬 CPU의 processor (논리적인 CPU ID) 값을 확인한 후 아래 명령어를 통해 처리하면 된다.



### 1) CPU ON

```shell
echo 1 > /sys/devices/system/cpu/cpu<processor id>/online
```



### 2) CPU OFF

```shell
echo 0 > /sys/devices/system/cpu/cpu<processor id>/online
```



**참고로 CPU0번은 위와 같이 같은 방법으로 제어할 수 없다.** 
즉, `/sys/devices/system/cpu/cpu0/online` 파일이 존재하지 않는다.





reference : [1](https://blog.naver.com/seuis398/70140453358)

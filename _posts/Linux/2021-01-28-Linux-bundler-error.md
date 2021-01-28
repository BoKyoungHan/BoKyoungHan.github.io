---
layout: post
title: "[Linux] 'Cant find gem bundler (>= 0.a) with executable bundle' 에러"
categories: [Linux, Troubleshooting]
tags: [linux, troubleshooting, bundler]
---

## Intro

깃 블로그에 필요한 환경설정을 할 때였다.

`Bundler`를 사용한 명령어를 실행시켰더니 아래와 같은 에러 메시지가 발생하는 것을 확인할 수 있었다.

```console
Can't find gem bundler (>= 0.a) with executable bundle (Gem::GemNotFoundException)
```

구글링 하다 발견한 방법 정리.



<br><br>

## Troubleshooting

참고한 사이트에는 세 가지 솔루션이 있었다. <br>그 중에서 정확한 번들러 버전을 설치하는 방법을 사용하니 효과가 있었다.

<br>

### Install the exact Bundler

> The only version of Bundler 100% guaranteed to work with a given `Gemfile.lock` file is the Bundler version that generated it. So the most reliable way to fix this error is to install that exact Bundler version. <br><br>This will be the default behavior of `bundle install` in the future, but for now you can get that result with:



<br>

```console
$ gem install bundler -v "$(grep -A 1 "BUNDLED WITH" Gemfile.lock | tail -n 1)"
```





<br><br><br>

reference: [1](https://bundler.io/blog/2019/05/14/solutions-for-cant-find-gem-bundler-with-executable-bundle.html)

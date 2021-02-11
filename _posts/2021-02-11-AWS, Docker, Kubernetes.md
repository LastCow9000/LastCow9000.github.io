---
title: 'AWS/ 도커/ 쿠버네티스란?'
categories: [BackEnd]
tags: [linux, server]
---

# AWS/ 도커/ 쿠버네티스란?

## container?

컨테이너는 **독립된 리눅스 환경을 보장받는** 프로세스다.  
( namespace 와 cgroup 을 적용한 프로세스 )

> namespace : 무엇을 볼 수 있는지(see) **제한**  
> cgroup : 얼마나 사용(use)가능 한지 **제한**

> ex) 웹 개발자 입장에서  
> 이것저것 깔아서 충돌나는 배포 환경을 고려하지 않아도 된다.  
> 운영자 입장에서는  
> 라이브러리 버전이 겹쳐도 상관없다.

App을 각각 컨테이너화  
<img src="https://raw.githubusercontent.com/LastCow9000/LastCow9000.github.io/master/_posts/images/02_App%20Containerization.jpg" width="450px" height="300px" title="App Containerization" alt="App Containerization"/>



## 도커, 컨테이너를 통한 여러대의 서버 관리에는 한계가 생긴다.

![many containers](C:\blog\LastCow9000.github.io\_posts\images\02_many containers.jpg)

이를 해결하기 위해 컨테이너 오케스트레이션 기술인 **쿠버네티스(Kubernetes)**가 만들어졌다.

> 1주일에 20억개 컨테이너를 생성하는 구글 서버 관리용
> borg 내부 도구를 2015년 오픈소스화.   

## AWS




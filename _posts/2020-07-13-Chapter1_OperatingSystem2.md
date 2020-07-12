---
title:  "운영체제 개요2"
excerpt: "운영체제 introduction"
comments: true

categories:
  - Operating System
tags: 
  - OS
toc: true
toc_sticky: true
last_modified_at:  2020-07-13 01:12:00 +0000
---

## Goal

> - 운영체제에 대한 관점 ( 자원 관리자, 프로세스, 계층 구조)를 이해하기
> - 인터럽트 (Interrupt) 이해하기

---

## 운영체제에 대한 관점 - 자원 관리자 관점

- **자원에 대한 수행 과정**
  - 자원의 상태를 추적 및 저장
  - 어떤 프로세스가 어떤 자원을 얼마나 사용할 것인지 결정하기 위한 정책 수립
  - 자원의 할당 및 회수

- **프로세스 관리 기능**
  - Process Scheduler
  - Process 상태 추적 및 저장

- **기억장치 관리 기능 / 정보 관리 기능**
- **장치 관리 기능**
  - 채널 등의 제어장치 및 입출력장치와 같은 각종 장치의 상태를 추적 및 저장
  - 입출력 스케줄링 (I/O Scehduling)

---

## 운영체제에 대한 관점 - 프로세스 관점

- 하나의 작업이 제시되어 완료될 때까지 하나의 프로세스에 대하여 그 상태를 변환시키고 관리한다.
  - 실행 중인 프로세스가 입출력이 완료될 때 까지 기다려야 한다면, 대기 상태의 프로세스로 변환되어야함. 
  - 운영체제는 작업이 완료될 때까지 관리해야 함

<img src="https://user-images.githubusercontent.com/32683894/87252765-ac2add80-c4b0-11ea-8dc4-63107863992a.png" alt="image" style="zoom:60%;" align="center" />

그림2. 다음 그림은 다중 프로그래밍 환경 하에서 존재할 수 있는 세 개의 프로세스(실행 중인 사용자 프로그램)를 나타낸 것이다.

---

## 운영체제에 대한 관점 - 계층 구조 관점

자원 관리 루틴이 어떻게 수행되고, 이 루틴들이 상호간에 어디에 논리적으로 위치하는 가를 알아야 한다. 

<img src="https://user-images.githubusercontent.com/32683894/87252880-73d7cf00-c4b1-11ea-9985-c77215b6d735.png" alt="image" style="zoom:67%;" align="center" />

---

## 입출력 프로그래밍 - Interrupt

**인터럽트 (Interrupt)**

- **시스템에 예기치 않은 상황이 발생하였을 때, 그것을 운영체제에 알리기 위한 메커니즘**
- **종류**
  - 입출력(I/O) Interrupt
  - 외부(external) Interrupt
  - SVC(SuperVisor Call) Interrupt
  - 기계 검사(machine check) Interrupt
  - 프로그램 에러(program error) Interrupt
  - 재시작(restart) Interrupt

<img src="https://user-images.githubusercontent.com/32683894/87253047-f44aff80-c4b2-11ea-9faf-436e3276cca6.png" alt="image" style="zoom:67%;"  align="center"/>

다음 그림은 인터럽트 처리 과정을 나타낸 것이다. 



## Reference

[KOCW 신한대학교 이광규 교수님 운영체제 강의](http://www.kocw.net/home/cview.do?cid=43cf05472bb2761a&ar=link_nvrc)

[참고한 도서 :  운영체제, 생능출판사, 박교석 외 4인](https://book.naver.com/bookdb/book_detail.nhn?bid=7294946)
---
title:  "[운영체제] Process 정의와 Process 상태도"
excerpt: "운영체제 process와 Thread"
comments: true

categories:
  - Operating System
tags: 
  - [OS, Process]
toc: true
toc_sticky: true
last_modified_at:  2020-07-13 01:12:00 +0000
---

## Goal

> - 프로세스 정의와 역할에 대해 이해한다.
> - 프로세스의 구성 요소가 무엇인지 안다.
> - 프로세스 Life Cycle을 이해한다.

---

## 1. Introduction

- 프로세스 스케쥴링 ( Process Scheduling)
  
  - 사용자로부터 의뢰받은 작업을 처리하기 위해 프로세스들에게 중앙처리장치 또는 프로세서들을 할당하기 위한 정책을 설정하는 것
  
- **목표 :** 중앙처리장치 효율 및 처리율(throughput)의 최대화와 반환시간(turnaround time)의 최소화

---

## 2. 프로세스 정의와 역할

- **프로세스(Process) 의 정의**

  - 실행중인 프로그램

  - PDB(Process Control Block)을 지닌 프로그램

  - PC(Program Counter)를 지닌 프로그램

  - 능동적 개체(entity)로, 순차적으로 수행하는 프로그램

    

하나의 프로세스는 CPU가 수행하는 작업 단위이다. 운영체제는 프로세스 관리와 관련해 다음과 같은 기능을 수행한다.

- **프로세스 (Process) 관리**
  - 사용자 프로세스와 시스템 프로세스의 생성과 삭제
  - 프로세스의 일지 중지와 재 수행
  - 프로세스 스케쥴링
  - 프로세스의 동기화
  - 프로세스 간 통신
  - 교착상태 처리 (Deadlock)

## 

## 3. 프로세스 구성 요소

임의의 프로그램이 실행되기 위해서는 반드시 실행되기 전에 주기억장치에 저장되어야 한다. 

- **프로세스 4가지 구성 요소**

  1. **코드(Code) 영역**
     - 프로그램 코드 자체 
     - 주기억장치에 CPU가 해석할 수 있는 Binary Code 상태로 올라가게 되는데 이 영역을 뜻한다.

  2. **데이터(Data) 영역**
     - 프로그램의 전역 변수(Global Variable)나 정적 변수(Static Variable)의 할당

  3. **스택(Stack) 영역**
     - 지역 변수(Local Variable) 할당과 함수 호출 시 전달되는 인수(Argument) 값

  4. **힙(Heap) 영역**
     - 동적 할당

<img src="https://user-images.githubusercontent.com/32683894/87295971-02476180-c541-11ea-8530-9a23e640c982.jpg" alt="프로세스 구성 요소" style="zoom:40%;" align = "center"/>

---

## 4. 프로세스 Life Cycle

1. **생성 (new)**
   - 프로세스가 생성되었지만 아직 승인 받지 못한 상태 (생성 중)
2. **준비완료 (Ready)**
   - 중앙처리장치가 사용 가능하게 될 때 그것을 할당받을 수 있는 상태

3. **실행 (Running)**
   - 프로세스가 중앙처리장치(CPU)를 차지하고 있는 상태
4. **대기 (Waiting)**
   - Running 상태 였다가 입출력 처리 등을 하게 되면, 중앙처리장치를 양도하고 입출력 처리가 완료될 때까지 대기하고 있는 상태 (특별한 사건을 기다림)

5. **종료 ( terminated)**
   - 프로세스 실행이 완료되고 할당된 CPU를 반납.



다음 그림은 프로세스 상태도이다. (Five-state)



<img src="https://user-images.githubusercontent.com/32683894/87304922-9240d780-c550-11ea-94b4-3a1a7394b42d.png" alt="image" style="zoom:60%;" />

**new -> ready** : OS에 의해 프로세스를 승인  - admitted 

**ready -> running** : 프로세스를 수행하기 위해 CPU 할당 - Scheduler dispatch

**running -> ready** : 할당된 시간이 지나면 timeout interrupt 발생 - interrupt

**running -> waiting** : timeout전에 I/O 요청 발생 - I/O or Event wait

**waiting -> ready** : I/O요청이 완료되면 다시 ready상타로 전이 - I/O or event completion

**running -> terminated** : 프로세스 종료 - exit



---

## Reference

[KOCW 신한대학교 이광규 교수님 운영체제 강의](http://www.kocw.net/home/cview.do?cid=43cf05472bb2761a&ar=link_nvrc)

[참고한 도서 :  운영체제, 생능출판사, 박교석 외 4인](https://book.naver.com/bookdb/book_detail.nhn?bid=7294946)
---
title:  "운영체제 개요1"
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

> - 운영체제 개요를 알아보자
> - 운영체제의 유형(역사)를 알아보자


---

## 운영체제란?

**운영체제란?**

- 컴퓨터 하드웨어와 컴퓨터 사용자 간의 매개체 역할을 하는 시스템 소프트웨어로서 사용자가 프로그램을 수행할 수 있는 환경을 제공한다.

**운영체제 목적**

- 컴퓨터 시스템을 편리하게 이용
- 컴퓨터 하드웨어를 효율적으로 관리

**운영체제의 관점**

- 자원 할당자라고도 함 
  - 컴퓨터 시스템을 공정하고 효율적으로 운영하기 위해 어떻게 자원을 할당할 것인가를 결정해줌
- 다양한 입출력장치와 사용자 프로그램의 통제자
  - 사용자 프로그램을 통제하여 오류 또는 컴퓨터의 부적저란 사용을 방지하는 것이다.



<img src="https://user-images.githubusercontent.com/32683894/87249486-5a775880-c49a-11ea-901a-26a7be09ad91.png" align="center" alt="image" style="zoom:65%;" />



하드웨어 - 중앙처리장치, 기억장치와 입출력장치로 구성되어 계산을 하기 위한 기본적인 자원을 제공

응용 프로그램 - 사용자가 제시한 문제를 풀기 위해 필요한 자원의 사용방법을 정의 

---

## 운영체제의 유형

- **일괄 처리 시스템 (Batch Processing System)**

  - 초기 컴퓨터는 오퍼레이터의 작업 준비 시간이 큰 문제가 되었다. - 중앙처리장치가 유휴 상태(idle state)가 되기 떄문

  - 유휴 상태의 시간을 없애기 위하여 작업 순서의 자동화(Automatic Job Sequencing) 개념을 도입함. 

    한 프로그램에서 다음 프로그램으로 제어를 자동적으로 넘기기 위해 만들어진 상주 모니터(resident monitor)를 두는 것 

  - 작업의 준비 및 실행 순서를 자동화함으로써 시스템의 성능을 증진함. 

  - 문제점: 

    - 하나의 작업이 시작되면, 그 작업이 모든 시스템 자원을 독점 사용함으로써 여러시스템 자원, 특히 중앙처리장치가 빈번한 유휴 시간을 가진다.
    
      

- **다중 프로그래밍 시스템 (Multi Programming System)**
  
  - 중앙처리장치가 항상 수행되도록 하여 그 이용도를 높이기 위한 방안
    -  작업은 입출력장치 등의 조작이 끝나는 것과 같은 어떤 사건(event)을 기다려야 할때가 있다. 
    -  비다중 프로그래밍체계하에서는 중앙처리장치가 쉬게되지만, 다중프로그래밍 체계하에서는 운영체제가 다른 작업으로 교환(switching) 하여 새로운 작업을 수행하도록 한다. 
  
  - 주기억장치 내에 여러 프로그램들이 존재하도록 함.
  
    
  
- **시분할 시스템 (Time-Sharing System)**
  
  - 터미널을 통하여 컴퓨터와 직접 접촉할 수 있도록 하기 위하여 개발되었다.
  - 사용자로 하여금 자신만이 컴퓨터 시스템을 독점하여 사용하고 있는 듯한 착각을 가지게 한다.
  - 즉, 여러 사용자들이 컴퓨터 자원에 대한 짧은 시간 단위의 공유
  - 사용자는 대화식(interactive) 단말장치를 이용하여 시분할 시스템과 인터페이스를 수행
  - 문제점:
    
    - 자원 제어에 대한 대부분의 책임을 운영체제에 전가시킴으로써 운영체제의 오버헤드가 커진다.
    
  
- **실시간 시스템 (Real-Time System)**
  
  - 매우 엄격하게 정의되어 있는 시간 제약 등과 같은 사건들의 제시된 상황을 분석
  - 사전에 정의된 제약 내에서 수행되어야 함
  
  - 특수 목적만을 위한 응용 분야에서 제어장치로 사용된다. (적의 공중 공격에 대비한 감시, 센서 등)
  
    
  
- **다중 처리 시스템 (Multi Processing System) = 병렬 시스템( Parallel System)**

  - 컴퓨터 시스템을 여러개의 프로세서로 구성하는 다중 처리 기법
    
  - 마이크로프로세서의 크기가 작아져 하나의 시스템에 여러개의 프로세서를 두는 것이 가능해졌기 떄문이다. 
    
  - 공유기억장치(Common Memory)를 통하여 하나로 연결된 다중 처리기(Multi Processor)의 제어 및 공유를 위한 시스템

  - 유형:

    - 프로세서들이 해당 작업을 처리함에 있어서 매우 밀접하게 동기화되어야하는 Tightly Coupled (밀착된 결합)

    - 두개 or 그 이상의 프로세스들만을 결합함으로써 높은 작업의 처리율(Throughput)을 제공하는데 목적을 둔 loosely Coupled(느슨한 결합)

      

- **개인용 컴퓨터 시스템 (Personal Computer System)**
  
  - 대형 시스템보다 작고 값이 싼 초소형 컴퓨터
  
- 중앙처리장치와 주변장치 이용률을 최대화 시키려는 노력 대신에 편리성과 응답성을 더 중요시 함. 
  
  - Microsoft - Windows XP : 새로운 하드웨어과 소프트웨어 설정을 쉽게할 수 있도록 지원
  
    
  
- **분산처리 시스템 (Distributed Processing System)**
  
  - 통신 네트워크를 통하여 서로 느슨히 결합된 프로세서들의 집함. 
  
- 자원을 가지고 있는 사이트는 서버가 되고, 다른 사이트에서의 Client들은  그 자원을 이요앟ㄴ다.
  
  - 자원 공유, 연상 속도 향상, 신뢰성 향상 및 통신 가능의 이점
  
    
  
- **멀티미디어 시스템 (Multimedia System)**
  
  - 다양한 미디어(이미지/그래픽, 사운드, 애니메이션 등)를 이용하여 멀티미디어 콘텐츠를 제작하기 위해 필요한 하드웨어와 소프트웨어로 구성

  - 멀티미디어 콘텐츠를 제작하기 위한 저작도구가 필요
  
    
  
- **임베디드 시스템 (Embedd System)**
  
  - 마이크로프로세서 or 마이크로컨트롤러를 내장하여 시스템 제작자가 의도한 몇 가지 혹은 특수한 기능만을 수행하도록 제작된 시스템





---

## Reference

[KOCW 신한대학교 이광규 교수님 운영체제 강의](http://www.kocw.net/home/cview.do?cid=43cf05472bb2761a&ar=link_nvrc)

[참고한 도서 :  운영체제, 생능출판사, 박교석 외 4인](https://book.naver.com/bookdb/book_detail.nhn?bid=7294946)
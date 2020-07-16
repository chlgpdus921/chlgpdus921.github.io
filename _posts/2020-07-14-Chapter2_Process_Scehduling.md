---
title:  "[운영체제] 프로세스 스케줄링"
excerpt: "운영체제 선점/비선점, 우선순위 등 다양한 스케줄링 기법을 알아보자"
comments: true

categories:
  - Operating System
tags: 
  - [OS, Process, Scheduling]
toc: true
toc_sticky: true
last_modified_at:  2020-07-14 03:15:00 +0000
---

## Goal

> - 프로세스 스케줄링 목적을 이해한다.
> - 프로세스 스케줄링 단계별 분류에 대해 알아보자
> - 선점/비선점, 우선순위, 기한부, 다중 프로세서 스케줄링을 알아보자

---

## 1. 프로세스 스케줄링 목적

- **공정성** : 스케줄링 방법이 공정해야하고, 어떤 프로세스도 무한 대기 상태가 되지 않아야 한다.
- **응답 시간의 최소화**
- **예측 가능** : 시스템 내의 부하(load)에 상관없이 거의 같은 비용, 같은 시간 내에 수행되어야 한다.
- **오버헤드의 최소화**
- **자원 사용의 균형 유지**
- **실행의 무한지연을 피할 것** : aging 기법 (자원을 오래 기다릴수록 우선순위를 높이는 방법)
- **주요 자원들을 차지하고 있는 프로세스에게 우선권을 부여** 
- **좀 더 바람직한 동작을 보이는 프로세스에게 더 좋은 서비스를 제공**: page fault율이 낮은 프로세스들에게 더 좋은 서비스 제공
- **우선순위제 실시** : 프로세스에 우선순위가 주어진 상황에서 스케줄링 기법은 높은 순위의 프로세스를 먼저 실행시킨다.

<br>

이렇게 많은 목적들은 서로 상충되는 결과를 발생함으로써, 스케줄링을 복잡하게 만드는 원인이 될 수 있다.



---

## 2. 프로세스 스케줄링 - 단계별 분류

1. **상위 단계 스케줄링 (High Level Scheduling)**

   - job 스케줄링 이라고도 불림
   - 어떤 작업에게 시스템의 자원들을 차지할 수 있도록 할 것인가를 결정한다.

2. **중간 단계 스케줄링 (Intermediate Level Scheduling)**

   - 어떤 프로세스들에게 중앙처리장치를 차지할 수 있도록 할 것인가를 결정한다.
   - 시스템 전체의 성능향상을 위하여 허용되는 시스템부하 내에서 짧은 순간에 프로세스들에 대한 일시적인 활동의 중단 및 재개를 수행한다. 
   - 시스템에서의 작업 승인과 작업들에 대한 중앙처리장치 할당 사이에서 버퍼역할을 한다.

3. **하위 단계 스케줄링 (Low Level Scheduling)**

   - 어떤 ready process에게 중앙처리장치를 할당할 것인가를 결정

   - 실제로 프로세스에게 할당해 준다.

     

---

## 3. 선점 / 비선점 스케줄링

1. **선점 (preemptive ) 스케줄링**
   - 하나의 프로세스가 중앙처리장치를 차지하고 있을 때 다른 프로세스가 현재 수행 중인 프로세스를 중지시키고 자신이 중앙처리장치를 차지할 수 있음.
   
   - 높은 우선순위를 가진 프로세스들이 빠른 처리를 요구하는 시스템에서 유용하다.
   
   - 시분할 시스템에서 선점 스케줄링으로 빠른 응답 시간을 보장해주는 것은 중요하다.
   
   - 하지만, Context Switching 으로 인한 오버헤드를 초래한다.
   
     

2. **비 선점 (nonpreemptive)  스케줄링**
   - 하나의 프로세스에 중앙처리장치가 할당되면, 그 프로세스의 수행이 끝날 때까지 빠져나올 수 없다.
   - 짧은 작업들이 긴 작업들에 의해서 기다리게 되지만, 모든 프로세스들에 대한 대우는 공정하다.
   - 도중에 높은 우선순위의 작업이 입력되더라도 대기 중인 작업들이 영향을 받지 않으므로 응답 시간을 쉽게 예측할 수 있다.

---

## 4. 우선순위(Priority) 스케줄링

- 각 프로세스에게 우선순위를 부여하여 우선순위가 높은 순서대로 처리하는 방법

1. **Static Priority**
   - 실행이 쉽고, 상대적으로 오버헤드는 적으나, 주위 여건의 변화에 적응하지 않고 우선순위를 바꾸지 않는다.
2. **Dynamic Priority**
   - 필요에 따라 우선순위를 재구성한다. Static Priority에 비해 복잡하고 오버헤드가 많아지지만, 시스템의 응답도를 증가시켜 처리 효율을 높인다.

---

## 5. 기한부(Deadline) 스케줄링

작업들이 명시된 시간이나 기한 내에 완료되도록 계획

1. **Hard real-time System**
   - 정한 시간 내에 완료할 수 있도록 해주는 강한 형태의 실시간 시스템 
   - 운영체제가 저장된 자료의 검색에서부터 시작하여 발생된 모든 요청을 완료할 때까지의 시스템 내의 모든 지연이 제한되도록함. 

2. **Soft real-time System**
   - 시간적 제한이 다소 약한 형태의 실시간 시스템
   - 중요한 task가 다른 task보다 높은 우선순위를 얻고, task가 완료될 때까지 우선순위를 계속 유지한다. 

- **정적 (Static) 스케줄링 방식**
  - 시스템에 의해 실행되는 task집합이 미리 정의되어 있는 경우. - Soft real-time System 에 유용
  - **RM (Rate Monotonic) 알고리즘**
    - 주기가 짧을수록 더 높은 우선순위를 부여한다.
- **동적 (Dynamic) 스케줄링 방식**
  - task 발생 시간이나 특성을 미리 예측할 수 없을 경우에 유용 - Hard real-time System 에 유용
  - **EDF(Earliest-Deadline First) 알고리즘**
    - 임계 시간이 가장 근접한 task를 가장 먼저 수행하는 방식

---

## 6. 다중 프로세서 (Multiple Processor) 스케줄링

지금까지는 단일 프로세서를 가진 시스템에서 중앙처리장치를 스케줄링하는 문제를 살펴보았다. 여러 개의 중앙처리장치가 사용 가능하게 되면, 스케줄링 문제는 더욱 복잡해진다. 다중 프로세서에 대해 논의해보자

- 프로세서들의 형태는 동질 시스템 or 이질 시스템 

  - 이질 시스템의 경우 각 프로세서는 자신의 큐가 있고 자신의 스케줄링 알고리즘을 가진다. 

- **동질 시스템일 경우, 부하를 공유함 (Load Sharing)**
  
- 한 개의 공동 큐로 들어가서 실행 가능한 프로세서에 스케줄된다.
  
- 이질 시스템일 경우

  1. 각 프로세서가 스스로 스케줄링하며, **공동 준비 큐**를 조사하여 실행할 프로세스를 선택한다.
- 두 프로세스가 동일한 프로세스를 선택하지 않도록 하며, 프로세스들이 큐에서 유실되지 않도록 보장해야한다.
  2. 한 프로세서가 다른 프로세서를 위한 스케줄러로서 지정되어 **주종 구조(Master Slave Structure)**를 구성한다.

  

---

## Reference

[KOCW 신한대학교 이광규 교수님 운영체제 강의](http://www.kocw.net/home/cview.do?cid=43cf05472bb2761a&ar=link_nvrc)

[참고한 도서 :  운영체제, 생능출판사, 박교석 외 4인](https://book.naver.com/bookdb/book_detail.nhn?bid=7294946)

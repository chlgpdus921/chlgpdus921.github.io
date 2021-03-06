---

title:  "[운영체제] 스레드(Thread) 와 멀티스레드(MultiThread)"
excerpt: "운영체제 스레드(Thread)의 특징 및 항목과 멀티스레드(MultiThread)에 대해 알아보자"
comments: true

categories:
  - Operating System
tags: 
  - [OS, Thread, MultiThread]
toc: true
toc_sticky: true
last_modified_at:  2020-07-15 13:15:00 +0000
---

## Goal

> - 스레드 (Thread) 개념에 대해 알아보자
> - 스레드 (Thread) 특징에 대해 알아보자
> - 스레드와 프로세스 포함 항목에 대해 이해한다.
> - 멀티 스레드 (Multi thread) 에 대해 알아보자

---

## 1. 스레드 (Thread) 

- 대부분 프로그램들의 경우, 서로 독립적인 일들을 불필요하게 순차적으로 수행하는 사실을 개선하기 위해 프로세스보다 작고 독립적으로 스케줄링이 가능한 스레드(CPU로 보내져 실행되는 단위)라는 개념이 도입되었다. 
- 여러 개의 프로세스를 사용하는 응용 프로그램의 경우 fork() 시스템 콜을 이용하여 새로운 프로세스를 생성함에 따라 상당히 많은 오버헤드를 발생시킨다. 
- 또한, 각 프로세스는 서로 독립된 주소 공간을 사용하기 때문에 프로세스 간 통신을 위해서는 메시지 큐, 세마포어, 공유 메모리 등의 시스템 자원을 사용해야만 한다. 
- 다중 스레드를 사용하는 경우, 하나의 프로세스에 많은 스레드가 존재할 수 있다.
- **스레드는 각각 독립적으로 실행할 수 있고, 각 스레드의 실행 순서는 시그널이나 동기화 방법을 통해서 제어된다.**
- 예시
  - 웹사이트에서 비디오를 보려고 할 때 스레드들 중 한 개는 다른 스트림이 비디오를 검색하는 동안, 배경음악을 검색할 수 있다. 세 번째 스레드는 배너광고에 나오는 애니메이션 광고를 갱신할 수 있다. 그리고 그것이 나타나는 동안 시스템은 이러한 모든 행위들이 동시에 수행된다. 
  - 그러나, CPU는 물리적으로 주어진 시간에 한 개 이상의 스레드를 실행할 수 없다. 한 스레드에서 다음 스레드로 매우 빠르게 교환(switch)되어 우리의 눈에는 동시에 서비스받는 것으로 보이는 것이다.

---

## 2. 스레드 (Thread) 특징

- 각 스레드는 서로 독립적이다.
- 스레드의 실행/종료 순서는 예측할 수 없다.
- 스레드들은 수행을 위해 스케줄 되고 결과들은 프로세스에게 전달된다.
- 프로그램에 있는 스레드의 수는 다른 스레드에게 알려지지 않는다.
- 스레드는 프로그램의 외부에서는 보이지 않는다.
- 스레드는 서로 독립적이지만, 한 스레드가 취한 행동은 프로세스에 있는 다른 스레드에 영향을 미친다.
- 스레드는 프로세스의 일부분이기 때문에 프로세스의 자원들을 공유하지만 자신만의 처리시간과 스택, 레지스터들이 할당된다.
- 한 프로세스가 exit( ) 시스템 콜을 통해 종료되면, 모든 스레드들도 종료된다.



---

## 3. 스레드 (Thread) 예시

각 프로세스는 자신의 PC와 스택, 레지스터들과 자신의 주소 공간을 갖는다. 대부분의 기존 프로그램들은 하나의 프로세스가 하나의 스레드를 갖는 형태로 구성된다. 

<img src="https://user-images.githubusercontent.com/32683894/87431587-d223bf80-c621-11ea-8fd1-e08663a97dc5.png" alt="image" style="zoom:60%;" />

---

## 4. 스레드와 프로세스 포함 항목

스레드는 주소 공간을 공유하는 것 외에도 개방된 파일과 자식 스레드, 타이머, 시그널 등을 공유하고 있다. 

- |                        스레드당 항목                         |                       프로세스당 항목                        |
  | :----------------------------------------------------------: | :----------------------------------------------------------: |
  | 스레드 식별자<br>PC<br>스택 포인터<br/>레지스터들<br/>자식 스레드<br/>스레드 상태 정보 | 주소 공간<br>전역 변수<br>개방된 파일들<br>자식 프로세스<br>시그널<br>세마포어<br>계정 정보 |

---

## 5. 멀티 스레드(Multi thread)

- **다수의 스레드를 이용하여 하나의 프로그램을 동시에 처리하는 것** 으로, 하나의 프로그램을 위하여 다수의 실행 단위를 이용한다는 점에서는 다중 프로세싱과 같은 의미이다. 
- 그러나 다중 프로세싱과 달리, 하나의 프로세스 자체에 다수의 실행 단위들이 존재하여, **작업의 수행에 필요한 자원들을 공유하기 때문에 자원의 생성 및 관리가 중복되는 것을 최소화할 수 있다.**
- 이러한 자원 공유는, 하나의 프로세스 내에서 뿐만 아니라 여러 개의 서로 다른 프로세스들 사이에서도 가능하다.
- 또한, 하나의 프로그램을 멀티 스레딩 기법을 이용할 경우, 각 스레드는 서로 독립적으로 동시에 수행이 가능하여 다중 프로세서 시스템에서는 물론, 단일 프로세서 시스템 상에서도 업무의 실질적인 다중 처리를 가능하게 한다.
- 예시
  - 다수의 클라이언트가 동시에 단일 웹 서버로 접속할 경우를 생각해 보자.
  - 스레드를 사용하지 않고 프로세스로 구현하는 상황이라면, 웹 서버는 한 사용자의 서비스 요청이 끝난 후에 다음 사용자에게 서비스를 제공해야 한다.
  - 마지막에 연결된 사용자는 앞선 사용자들의 요청이 끝난 뒤 제공받을 수있다. 그러나 멀티 스레드로 서비스를 제공한다면 클라이언트들은 기다릴 필요가 없다.
- 중량 프로세스(HWP : Heavy Weight Process) - 하나의 스레드를 가진 프로세스
- 경량 프로세스(LWP : Light Weight Process) - 프로세스 내에 두 개 이상의 스레드를 포함하고 있을 경우
  - 같은 프로그램 코드, 데이터, 시스템 자원들을 이용하는 반면, 각각의 pc, 레지스터들과 스택을 가진다. 단일 프로세서 사의 메모리나 다중 프로세서 상의 단일 공유 메모리에서 실행된다. 
  - 공유된 자원과 연관되어 있는 복수 개의 스레드를 제어하는 문제가 있다. 
- KLT(Kernel-level threads)방법
  - Mach, OS2, Linux, Unix, Windows 등에서는 스레드들이 커널에 의하여 지원

- ULT(User-level threads)방법
  - POSIX(Portable OS Interface)는 사용자 수준에서 라이브러리 호출 집합을 통하여 커널의 상위 수준에서 지원



---

## Reference

[KOCW 신한대학교 이광규 교수님 운영체제 강의](http://www.kocw.net/home/cview.do?cid=43cf05472bb2761a&ar=link_nvrc)

[참고한 도서 :  운영체제, 생능출판사, 박교석 외 4인](https://book.naver.com/bookdb/book_detail.nhn?bid=7294946)

제시된 그림은 도서를 참고하여 직접 제작했다.


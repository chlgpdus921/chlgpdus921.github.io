---
title:  "[운영체제] PCB와 프로세스 생성"
excerpt: "운영체제 PCB와 fork()명령어에 대해 알아보자"
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

> - 프로세서 제어 블록 PCB에 대해 이해한다.
> - 프로세스 생성 fork() 명령어를 이해한다.

---

## 1. 프로세스 제어 블록 (PCB)

- **프로세스 제어 블록 (Process Control Block) :  프로세스에 관한 모든 정보를 가지고 있는 데이터베이스**

- PCB는 프로세스 생성 시에 만들어진다. 즉, **모든 프로세스는 각기 고유의 PCB를 지닌다.**
- 프로세스 수행이 완료되면, 해당 PCB는 제거된다. 
- **프로세스는 CPU가 처리하던 작업의 내용들을 자신의 PCB에 저장하고, 다음에 다시 CPU를 점유하여 작업을 수행해야 할 때 해당 정보들을 CPU에 넘겨 계속해서 하던 작업을 진행 할 수 있다.**

- **PCB 내용** 

  - **Pointer** : 부모 프로세스에 대한 포인터, 자식 프로세스에 대한 포인터, 프로세스가 적재된 기억장치의 주소를 가지는 포인터
  - **Process State** : 프로세스의 현재 상태 (running, ready, waiting)

  - **Process Number** : 프로세스가 생성될 때 부여받는 고유 식별자 (indentifier)
  - **Program Counter** : 프로세스가 다음에 수행해야할 명령어의 주소
  - **Registers** : 중앙처리장치의 각종 레지스터 상태를 저장하기 위한 공간

<img src="https://user-images.githubusercontent.com/32683894/87313931-8b6c9180-c55d-11ea-9b37-1304dce4631e.jpg" alt="pcb" style="zoom:40%;" />



---

## 2. 프로세스 생성

유닉스 환경에서 프로세스를 생성시키는 것은 fork() 명령어이다. 

하나의 프로그램이 실행하는 도중에 fork() 명령어를 실행하게 되면 동시에 두개의 프로그램으로 나누어져 실행하게 된다. 

이때 새로운 프로그램을 생성시킨 프로그램을 부모 프로세스 (Parent Process), 생성된 프로그램을 자식 프로세스 (Child Process)라고 한다. 즉, 부모 프로세스가 fork()명령어를 실행하게 되면 부모와 똑같은 자식 프로세스가 생성된다. 

<img src="https://user-images.githubusercontent.com/32683894/87317598-30896900-c562-11ea-9fd3-f3bfd59a9150.jpg" alt="fork" style="zoom:33%;" />

다음 그림을 보자. 

fork()명령어 이후에 두개의 프로세스가 수행되고 있다. PC는 다음에 수행되어야 할 명령어의 주소 값이 들어있는 레지스터이다. fork()전에는 PC가 1개인데, fork()이후에는 프로세스가 두 개가 되므로, 다음 실행될 명령어가 두 개이고, 각각의 PC가 있음을 알 수 있다. 



그렇다면, Quiz!! 어떤 순서로 차례대로 print 될까? 

다음 코드를 리눅스 환경에 작성해보자. unistd.h 헤더는 리눅스 환경에서만 작성될 수 있다. 

<img src="https://user-images.githubusercontent.com/32683894/87331896-b19e2b80-c575-11ea-95c3-f43a59598017.jpg" alt="fork명령어" style="zoom:40%;" />

```c
#include <stdio.h>
#include <unistd.h>
int main() {
	pid_t pid;
    
	printf("Before fork...\n");

	pid = fork(); //0일 경우 자식 // 양수일 경우 부모
	if (pid == 0)
		printf("I'm the Child ... pid is %d \n", pid);
	else if (pid > 0) {
		wait(NULL); //자식 프로세스의 수행이 완료된 후 부모 프로세스를 수행시킬 때 처리. 
		printf("I'm the Parent ... pid is %d \n", pid);
	}
	else
		printf("fork error");

	return 0;
}
```


결과창 

```
I'm the Parent ... pid is 46834

I'm the Child ... pid is 46838
```

Wait(NULL)를 적용시켰을 때 

```
I'm the Child ... pid is 46838

I'm the Parent ... pid is 46834
```



---

## Reference

[KOCW 신한대학교 이광규 교수님 운영체제 강의](http://www.kocw.net/home/cview.do?cid=43cf05472bb2761a&ar=link_nvrc)

[참고한 도서 :  운영체제, 생능출판사, 박교석 외 4인](https://book.naver.com/bookdb/book_detail.nhn?bid=7294946)

제시된 그림들은 모두 자료를 보며, 직접 제작했다. made by hyeyeon
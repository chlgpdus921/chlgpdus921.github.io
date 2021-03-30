---
title:  "jenv로 java version 변경하기 (JDK 버전 관리)"
excerpt: "터미널로 java version 변경하기"
comments: true

categories:
  - java
tags: 
  - [java]
toc: true
toc_sticky: true
last_modified_at:  2021-02-21 03:15:00 +0000
---

---

## 서론 

이 게시물을 보는 사람은 여러 방법을 시도했음에도 불구하고, 안돼서 다른 방법을 찾으러 온 사람일 것이다. 잘왔습니다!! 여기가 정답입니댜!!!



우선 필자의 개발환경은 이렇다. : MAC, Terminal- irteam

내가 기존에 시도한 방법은 이렇다. 

1. 다음과 같은 명령어를 입력해서 내 local에 어떤 java-version들이 있는지 확인하자. 

```bash
%  /usr/libexec/java_home -V
```

```bash
Matching Java Virtual Machines (2):
    11.0.9.1, x86_64:	"AdoptOpenJDK 11"	/Library/Java/JavaVirtualMachines/adoptopenjdk-11.jdk/Contents/Home
    11.0.2, x86_64:	"OpenJDK 11.0.2"	/Library/Java/JavaVirtualMachines/jdk-11.0.2.jdk/Contents/Home/Library/Java/JavaVirtualMachines/adoptopenjdk-11.jdk/Contents/Home
```

2. 편집기를 켜서 아래처럼 입력하자. 

```bash
# 편집기 실행
vi ~/.zshrc

# 변경하고 싶은 버전 입력
export JAVA_HOME=$(/usr/libexec/java_home -v 11.0.9.1) 
```

3. 입력 후, 버전을 확인 해보자

```bash
source ~/.zshrc
echo $JAVA_HOME
java -version
```



대부분의 블로그 글은 이렇다. 근데 내가 기존에 설정한 것이 잘못돼서 그런지 이 방법이 먹히지 않았다.  

나처럼 version이 바뀌지 않는 이들은 아래처럼 시도해보자



## 해결

```bash
#바꾸고 싶은 version의 폴더명 이름을 바꿔 넣어주자. ( 명령어: ls)
# jenv add /Library/Java/JavaVirtualMachines/{jdk폴더명}/Contents/Home/
jenv add /Library/Java/JavaVirtualMachines/jdk-11.0.9.1jdk/Contents/Home/

#변경할 버전 넘버
#11이라고 써도 무방하다. 
jenv global 11.0.9.1
```

입력한 뒤 java -version으로 확인해보자. 굿 매우 잘 바뀌었다.

![스크린샷 2021-03-30 오후 2 46 16](https://user-images.githubusercontent.com/32683894/112939603-b9831780-9166-11eb-9df6-878c46d2ce19.png)






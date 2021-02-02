---
title:  "vi tutorial 교육 내용 요약"
excerpt: "NHN basecamp vi tutorial 수업 요약입니다."
comments: true

categories:
  - basecamp
tags: 
  - [basecamp]
toc: true
toc_sticky: true
last_modified_at:  2021-01-21 03:15:00 +0000

---

## Goal

> - 단축키를 이해하고 연습해보자 

---

### Cursor

[[ : 파일의 첫번째

]] : 파일의 마지막

0 : 라인의 첫번째

$ : 라인의 마지막

M : page 중간

H : page 위

L : page 마지막

### Editing

- insert, append, open line
  - i, a, o

- Delete
  - dd : 한줄 다 지우기
  - dw : 단어 하나 삭제 
  - x : 단어 하나 삭제

- Undo - u 

- Redo - Ctrl-r

- Combination
  - 4dd : 지금 커서부터 끝까지 지워라 
  - dG : 현재 위치부터 파일 끝까지 다지워라 
  - 5x : 5글자를 지워라 

- Repetition
  - . : 마지막으로 했던 명령어를 반복함. 
  - Ex) dd 누르고, . 만 계속 누르면 계속 삭제 

---

### Search

/string : 위에서부터 서치

?string : 아래서부터 서치 

n : action 반복 



### Termination 

Save and or die

:wq 저장하고 나가기

:w <filename>

- vim test.txt 파일 생성해서 들어가서, 작성 후 저장할 때 명령어 입력

:q!  :저장안하고 나가기



### Reload

실시간으로 새로 덧붙여 지는 로그를 확인하고 싶을 때

:e 

---

### Replace

- 파일 전체에 대해 특정 단어를 치환
  - : %s/string/replace
  - : %s/string/replace/[option]
    - option
      - 대소문자 구분 없이 : i
      - 하나의 단어에 여러 개의 반복 문자 치환 : g

- 10행부터 25행까지만 치환
  - :10,25s/string/replace/
- 현재 행부터 마지막 행까지 치환
  - :.,$s/string/replace/

---

### Split

- vi로 보고 있는 파일의 여러 부분을 한 눈에 보고 싶음
  - :sp[lit] - 수직 창 분할
  - :vs[plit] - 수평 창 분할
  - :sp 파일명 - 새로운 창에서 open

- 분할 된 창에서 cursor 이동
  - Ctrl + w, w
- 분할 된 창 닫기
  - :close

---

### Yank

yy & p : copy & paste



y'a :  특정 라인부터 현재 커서까지 복사

d'a : 특정 라인부터 현재 커서까지 삭제



---

### Customization

:set nu - 문서 라인수 보이게 하기 

:set fileencoding=utf8 (한글이 깨져있을 떄)

---

### Reference

교육명 : NHN basecamp vi tutorial class

강사님 성함 : 김기남 책임님

교육 요약 내용입니다. (좋은 교육 감사합니다!)
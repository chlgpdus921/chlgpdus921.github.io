---

title:  "[프로그래머스-MySQL] 입양 시각 구하기(1) LEVEL 2"
excerpt: "입양 시각 구하기(1) 문제 풀이, GROUP BY"
comments: true

categories:
  - Programmers
tags: 
  - [MySQL, Database, Programmers]
toc: true
toc_sticky: true
last_modified_at:  2020-09-03 04:15:00 +0000
---

## Goal

> - 풀이를 보고 난 후 문제를 풀 수 있다.

## 문제

`ANIMAL_OUTS` 테이블은 동물 보호소에서 입양 보낸 동물의 정보를 담은 테이블입니다. `ANIMAL_OUTS` 테이블 구조는 다음과 같으며, `ANIMAL_ID`, `ANIMAL_TYPE`, `DATETIME`, `NAME`, `SEX_UPON_OUTCOME`는 각각 동물의 아이디, 생물 종, 입양일, 이름, 성별 및 중성화 여부를 나타냅니다.

| NAME             | TYPE       | NULLABLE |
| ---------------- | ---------- | -------- |
| ANIMAL_ID        | VARCHAR(N) | FALSE    |
| ANIMAL_TYPE      | VARCHAR(N) | FALSE    |
| DATETIME         | DATETIME   | FALSE    |
| NAME             | VARCHAR(N) | TRUE     |
| SEX_UPON_OUTCOME | VARCHAR(N) | FALSE    |

보호소에서는 몇 시에 입양이 가장 활발하게 일어나는지 알아보려 합니다. 09:00부터 19:59까지, 각 시간대별로 입양이 몇 건이나 발생했는지 조회하는 SQL문을 작성해주세요. 이때 결과는 시간대 순으로 정렬해야 합니다.

##### 예시

SQL문을 실행하면 다음과 같이 나와야 합니다.

| HOUR | COUNT |
| ---- | ----- |
| 9    | 1     |
| 10   | 2     |
| 11   | 13    |
| 12   | 10    |
| 13   | 14    |
| 14   | 9     |
| 15   | 7     |
| 16   | 10    |
| 17   | 12    |
| 18   | 16    |
| 19   | 2     |



## 풀이

- 구해야 할 것  
  - 09:00부터 19:59까지, 각 시간대별로 입양이 몇 건이나 발생했는가
  - 결과는 시간대 순으로 정렬 (=ORDER BY ASC)



나에겐 난이도 있는 문제였다.

DATETIME을 시간대별로 그룹을 묶어줘야 하는데 HOUR이라는 함수가 존재한다.

HOUR을 그룹으로 묶어준 후, 그 그룹이 몇개인지 COUNT해주면 된다. 



**공부하는 김에 다른 함수도 살펴보자.**

> YEAR(DATETIME) - 년도 (1000-9999)
>
> HOUR(DATETIME) - 시간 (0-23)
>
> MINUTE(DATETIME) - 분 (0-59)
>
> SECOND(DATETIME) - 초 (0-59)

```sql
SELECT HOUR(DATETIME) AS HOUR, COUNT(DATETIME) AS COUNT
FROM ANIMAL_OUTS
GROUP BY HOUR
ORDER BY HOUR;
```

이 형식으로 실행할시 09:00~19:59조건에 위배되는 결과가 뜬다. 

조건문 잊지말고 써주기!!!

<img src="https://user-images.githubusercontent.com/32683894/92146458-b7690c80-ee54-11ea-86b2-e2fb0a2c3428.png" alt="image" style="zoom:50%;" />

```sql
SELECT HOUR(DATETIME) AS HOUR, COUNT(DATETIME) AS COUNT
FROM ANIMAL_OUTS
GROUP BY HOUR
HAVING HOUR >=9 AND HOUR <=19
ORDER BY HOUR;
```



---

## Reference

[[프로그래머스] 입양 시각 구하기(1)](https://programmers.co.kr/learn/courses/30/lessons/59412)


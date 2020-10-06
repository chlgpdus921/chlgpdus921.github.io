---

title:  "[프로그래머스-MySQL] 있었는데요 없었습니다 LEVEL 3"
excerpt: "있었는데요 없었습니다 문제 풀이, JOIN"
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

`ANIMAL_INS` 테이블은 동물 보호소에 들어온 동물의 정보를 담은 테이블입니다. `ANIMAL_INS` 테이블 구조는 다음과 같으며, `ANIMAL_ID`, `ANIMAL_TYPE`, `DATETIME`, `INTAKE_CONDITION`, `NAME`, `SEX_UPON_INTAKE`는 각각 동물의 아이디, 생물 종, 보호 시작일, 보호 시작 시 상태, 이름, 성별 및 중성화 여부를 나타냅니다.

| NAME             | TYPE       | NULLABLE |
| ---------------- | ---------- | -------- |
| ANIMAL_ID        | VARCHAR(N) | FALSE    |
| ANIMAL_TYPE      | VARCHAR(N) | FALSE    |
| DATETIME         | DATETIME   | FALSE    |
| INTAKE_CONDITION | VARCHAR(N) | FALSE    |
| NAME             | VARCHAR(N) | TRUE     |
| SEX_UPON_INTAKE  | VARCHAR(N) | FALSE    |

`ANIMAL_OUTS` 테이블은 동물 보호소에서 입양 보낸 동물의 정보를 담은 테이블입니다. `ANIMAL_OUTS` 테이블 구조는 다음과 같으며, `ANIMAL_ID`, `ANIMAL_TYPE`, `DATETIME`, `NAME`, `SEX_UPON_OUTCOME`는 각각 동물의 아이디, 생물 종, 입양일, 이름, 성별 및 중성화 여부를 나타냅니다. `ANIMAL_OUTS` 테이블의 `ANIMAL_ID`는 `ANIMAL_INS`의 `ANIMAL_ID`의 외래 키입니다.

| NAME             | TYPE       | NULLABLE |
| ---------------- | ---------- | -------- |
| ANIMAL_ID        | VARCHAR(N) | FALSE    |
| ANIMAL_TYPE      | VARCHAR(N) | FALSE    |
| DATETIME         | DATETIME   | FALSE    |
| NAME             | VARCHAR(N) | TRUE     |
| SEX_UPON_OUTCOME | VARCHAR(N) | FALSE    |

관리자의 실수로 일부 동물의 입양일이 잘못 입력되었습니다. 보호 시작일보다 입양일이 더 빠른 동물의 아이디와 이름을 조회하는 SQL문을 작성해주세요. 이때 결과는 보호 시작일이 빠른 순으로 조회해야합니다.

##### 예시

예를 들어, `ANIMAL_INS` 테이블과 `ANIMAL_OUTS` 테이블이 다음과 같다면

```
ANIMAL_INS
```

| ANIMAL_ID | ANIMAL_TYPE | DATETIME            | INTAKE_CONDITION | NAME     | SEX_UPON_INTAKE |
| --------- | ----------- | ------------------- | ---------------- | -------- | --------------- |
| A350276   | Cat         | 2017-08-13 13:50:00 | Normal           | Jewel    | Spayed Female   |
| A381217   | Dog         | 2017-07-08 09:41:00 | Sick             | Cherokee | Neutered Male   |

```
ANIMAL_OUTS
```

| ANIMAL_ID | ANIMAL_TYPE | DATETIME            | NAME     | SEX_UPON_OUTCOME |
| --------- | ----------- | ------------------- | -------- | ---------------- |
| A350276   | Cat         | 2018-01-28 17:51:00 | Jewel    | Spayed Female    |
| A381217   | Dog         | 2017-06-09 18:51:00 | Cherokee | Neutered Male    |

SQL문을 실행하면 다음과 같이 나와야 합니다.

| ANIMAL_ID | NAME     |
| --------- | -------- |
| A381217   | Cherokee |



## 풀이

- 구해야 할 것  
  -   보호 시작일보다 입양일이 더 빠른 동물의 아이디와 이름을 조회
  -  보호 시작일(ANIMAL_INS) 이 빠른 순으로 조회 ( = ORDER BY A.DATETIME)

[[MySQL] Join (Outer Join, Inner Join) 설명 및 예제](https://chlgpdus921.github.io/mysql/MySQL-JOIN/)   <---- 문제를 풀기 전 다음 글을 읽고오자.

테이블이 2개나 생겼다. 내용을 정리해보자. ( JOIN문제는 글로 정리하고 그림 그리는게 쉽다.)

1. ANIMAL_INS : 동물 보호소에 들어온 동물의 정보
2. ANIMAL_OUTS : 동물 보호소에서 입양 보낸 동물의 정보

보호시작일  = ANIMAL_INS 테이블의 DATETIME

입양일 = ANIMAL_OUTS  테이블의 DATETIME

- 보호시작일보다 입양일이 더 빠르다?
  - **ANIMAL_INS와 ANIMAL_OUTS 테이블 모두 존재해야하는 정보**
  - ANIMAL_INS (A) 보다 **ANIMAL_OUTS (B) 의 DATETIME이 작아야 한다.**



<img src="https://user-images.githubusercontent.com/32683894/91835533-7de1a700-ec84-11ea-9435-2d0c66b2ed5d.png" alt="image" style="zoom:50%;" />

다음과 같은 그림을 생각할 수있다.

A와 B의 교집합은 OUTER JOIN이 아닌 INNER JOIN (외우자! 교집합은 INNER)

INNER JOIN형식을 그대로 써준 뒤 WHERE에 DATETIME만 비교해주면 된다.

(이해가 안된다면 첨부된 링크를 보고 형식을 이해하고 오자!)

```sql
SELECT B.ANIMAL_ID, B.NAME
FROM ANIMAL_INS A INNER JOIN ANIMAL_OUTS B
ON A.ANIMAL_ID = B.ANIMAL_ID
WHERE B.DATETIME < A.DATETIME 
ORDER BY A.DATETIME;
```

---

## Reference

[[프로그래머스] 없어진 기록 찾기](https://programmers.co.kr/learn/courses/30/lessons/59042)

[[MySQL] Join (Outer Join, Inner Join) 설명 및 예제](https://chlgpdus921.github.io/mysql/MySQL-JOIN/)


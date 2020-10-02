---

title:  "[프로그래머스-MySQL] 오랜 기간 보호한 동물(1) LEVEL 3"
excerpt: "오랜 기간 보호한 동물(1) 문제 풀이, JOIN"
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

아직 입양을 못 간 동물 중, 가장 오래 보호소에 있었던 동물 3마리의 이름과 보호 시작일을 조회하는 SQL문을 작성해주세요. 이때 결과는 보호 시작일 순으로 조회해야 합니다.

##### 예시

예를 들어, `ANIMAL_INS` 테이블과 `ANIMAL_OUTS` 테이블이 다음과 같다면

```
ANIMAL_INS
```

| ANIMAL_ID | ANIMAL_TYPE | DATETIME            | INTAKE_CONDITION | NAME   | SEX_UPON_INTAKE |
| --------- | ----------- | ------------------- | ---------------- | ------ | --------------- |
| A354597   | Cat         | 2014-05-02 12:16:00 | Normal           | Ariel  | Spayed Female   |
| A373687   | Dog         | 2014-03-20 12:31:00 | Normal           | Rosie  | Spayed Female   |
| A412697   | Dog         | 2016-01-03 16:25:00 | Normal           | Jackie | Neutered Male   |
| A413789   | Dog         | 2016-04-19 13:28:00 | Normal           | Benji  | Spayed Female   |
| A414198   | Dog         | 2015-01-29 15:01:00 | Normal           | Shelly | Spayed Female   |
| A368930   | Dog         | 2014-06-08 13:20:00 | Normal           |        | Spayed Female   |

```
ANIMAL_OUTS
```

| ANIMAL_ID | ANIMAL_TYPE | DATETIME            | NAME  | SEX_UPON_OUTCOME |
| --------- | ----------- | ------------------- | ----- | ---------------- |
| A354597   | Cat         | 2014-05-02 12:16:00 | Ariel | Spayed Female    |
| A373687   | Dog         | 2014-03-20 12:31:00 | Rosie | Spayed Female    |
| A368930   | Dog         | 2014-06-13 15:52:00 |       | Spayed Female    |

SQL문을 실행하면 다음과 같이 나와야 합니다.

| NAME   | DATETIME            |
| ------ | ------------------- |
| Shelly | 2015-01-29 15:01:00 |
| Jackie | 2016-01-03 16:25:00 |
| Benji  | 2016-04-19 13:28:00 |

※ 입양을 가지 못한 동물이 3마리 이상인 경우만 입력으로 주어집니다.



## 풀이

- 구해야 할 것  
  -   입양을 못 간 동물 중, 가장 오래 보호소에 있었던 동물 3마리의 이름과 보호 시작일을 조회
  -   보호 시작일(ANIMAL_INS TABLE) 순으로 조회  ( = ORDER BY A.DATETIME)

[[MySQL] Join (Outer Join, Inner Join) 설명 및 예제](https://chlgpdus921.github.io/mysql/MySQL-JOIN/)   <---- 문제를 풀기 전 다음 글을 읽고 오자.

테이블이 2개나 생겼다. 내용을 정리해보자. ( JOIN문제는 글로 정리하고 그림 그리는게 쉽다.)

1. ANIMAL_INS : 동물 보호소에 들어온 동물의 정보
2. ANIMAL_OUTS : 동물 보호소에서 입양 보낸 동물의 정보

입양을 못 간 동물  = ANIMAL_OUTS 테이블 정보

가장 오래 보호소에 있던 동물  = ANIMAL_INS  테이블 정보

- 입양을 못 간 동물 중, 가장 오래있던 동물 3마리 
  - **ANIMAL_OUTS에 없는 동물이고, ANIMAL_INTS 에는 존재하며 DATETIME이 가장 오래전인 동물**
  - ANIMAL_INS (A) 에는 있고,  ANIMAL_OUTS (B) 에는 없다.



<img src="https://user-images.githubusercontent.com/32683894/91834764-6eae2980-ec83-11ea-8745-cb69161157d5.png" alt="image" style="zoom:50%;" />

다음과 같은 그림을 생각할 수있다.

- 왼쪽이 색칠되어 있네 => LEFT JOIN

- ONLY A만 이네! WHERE에 B.KEY IS NULL 넣어주기 
- 동물 3마리 뽑기는 LIMIT 3;

(이해가 안된다면 첨부된 링크를 보고 형식을 이해하고 오자!)

```sql
SELECT A.NAME, A.DATETIME
FROM ANIMAL_INS A LEFT JOIN ANIMAL_OUTS B
ON A.ANIMAL_ID = B.ANIMAL_ID
WHERE B.ANIMAL_ID IS NULL
ORDER BY A.DATETIME
LIMIT 3; -- 동물 3마리 뽑기
```

---

## Reference

[[프로그래머스] 오랜 기간 보호한 동물(1)](https://programmers.co.kr/learn/courses/30/lessons/59044)

[[MySQL] Join (Outer Join, Inner Join) 설명 및 예제](https://chlgpdus921.github.io/mysql/MySQL-JOIN/)


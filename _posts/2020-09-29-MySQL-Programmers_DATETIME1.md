---


title:  "[프로그래머스-MySQL] 오랜 기간 보호한 동물 LEVEL 3"
excerpt: "오랜 기간 보호한 동물, DATETIME"
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

입양을 간 동물 중, 보호 기간이 가장 길었던 동물 두 마리의 아이디와 이름을 조회하는 SQL문을 작성해주세요. 이때 결과는 보호 기간이 긴 순으로 조회해야 합니다.

##### 예시

예를 들어, `ANIMAL_INS` 테이블과 `ANIMAL_OUTS` 테이블이 다음과 같다면

```
ANIMAL_INS
```

| ANIMAL_ID | ANIMAL_TYPE | DATETIME            | INTAKE_CONDITION | NAME       | SEX_UPON_INTAKE |
| --------- | ----------- | ------------------- | ---------------- | ---------- | --------------- |
| A354597   | Cat         | 2014-05-02 12:16:00 | Normal           | Ariel      | Spayed Female   |
| A362707   | Dog         | 2016-01-27 12:27:00 | Sick             | Girly Girl | Spayed Female   |
| A370507   | Cat         | 2014-10-27 14:43:00 | Normal           | Emily      | Spayed Female   |
| A414513   | Dog         | 2016-06-07 09:17:00 | Normal           | Rocky      | Neutered Male   |

```
ANIMAL_OUTS
```

| ANIMAL_ID | ANIMAL_TYPE | DATETIME            | NAME       | SEX_UPON_OUTCOME |
| --------- | ----------- | ------------------- | ---------- | ---------------- |
| A354597   | Cat         | 2014-06-03 12:30:00 | Ariel      | Spayed Female    |
| A362707   | Dog         | 2017-01-10 10:44:00 | Girly Girl | Spayed Female    |
| A370507   | Cat         | 2015-08-15 09:24:00 | Emily      | Spayed Female    |

SQL문을 실행하면 다음과 같이 나와야 합니다.

| ANIMAL_ID | NAME       |
| --------- | ---------- |
| A362707   | Girly Girl |
| A370507   | Emily      |

※ 입양을 간 동물이 2마리 이상인 경우만 입력으로 주어집니다.

---

## 풀이

- 구해야 할 것  
  -   입양을 간 동물 중, 보호 기간이 가장 길었던 동물 두 마리의 아이디와 이름을 
  -   결과는 보호 기간이 긴 순으로 조회

테이블이 2개나 생겼다. 내용을 정리해보자. ( JOIN문제는 글로 정리하고 그림 그리는게 쉽다.)

1. ANIMAL_INS : 동물 보호소에 들어온 동물의 정보
2. ANIMAL_OUTS : 동물 보호소에서 입양 보낸 동물의 정보



입양을 간 동물 = ANIMAL_OUTS TABLE

보호 기간이 가장 길었던 동물 = ANIMAL_INS TABLE

- ANIMAL_INS , ANIMAL_OUTS 테이블 두 개에 모두 정보가 있어야하고 그 중 보호기간이 긴 동물을 구하면 된다.
- 두 개에 모두 정보가 있다 = 교집합 = INNER JOIN
- 보호기간이 가장 길다 = > 입양 간 DATETIME - 보호 DATETIME  = 가장 커야함 = 내림차순 정렬

```sql
SELECT A.ANIMAL_ID, A.NAME
FROM ANIMAL_INS A INNER JOIN ANIMAL_OUTS B ON A.ANIMAL_ID = B.ANIMAL_ID 
ORDER BY (B.DATETIME - A.DATETIME) DESC
LIMIT 2;
```

---

## Reference

[[프로그래머스] 오랜 기간 보호한 동물 ](https://programmers.co.kr/learn/courses/30/lessons/59411)


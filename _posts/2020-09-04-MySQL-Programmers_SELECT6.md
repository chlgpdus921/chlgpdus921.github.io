---

title:  "[프로그래머스-MySQL] 여러 기준으로 정렬하기 LEVEL 1"
excerpt: "여러 기준으로 정렬하기 문제 풀이, SELECT"
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

동물 보호소에 들어온 모든 동물의 아이디와 이름, 보호 시작일을 이름 순으로 조회하는 SQL문을 작성해주세요. 단, 이름이 같은 동물 중에서는 보호를 나중에 시작한 동물을 먼저 보여줘야 합니다.

##### 예시

예를 들어, `ANIMAL_INS` 테이블이 다음과 같다면

| ANIMAL_ID | ANIMAL_TYPE | DATETIME            | INTAKE_CONDITION | NAME  | SEX_UPON_INTAKE |
| --------- | ----------- | ------------------- | ---------------- | ----- | --------------- |
| A349996   | Cat         | 2018-01-22 14:32:00 | Normal           | Sugar | Neutered Male   |
| A350276   | Cat         | 2017-08-13 13:50:00 | Normal           | Jewel | Spayed Female   |
| A396810   | Dog         | 2016-08-22 16:13:00 | Injured          | Raven | Spayed Female   |
| A410668   | Cat         | 2015-11-19 13:41:00 | Normal           | Raven | Spayed Female   |

1. 이름을 사전 순으로 정렬하면 다음과 같으며, 'Jewel', 'Raven', 'Sugar'
2. 'Raven'이라는 이름을 가진 개와 고양이가 있으므로, 이 중에서는 보호를 나중에 시작한 고양이를 먼저 조회합니다.

따라서 SQL문을 실행하면 다음과 같이 나와야 합니다.

| ANIMAL_ID | NAME  | DATETIME            |
| --------- | ----- | ------------------- |
| A350276   | Jewel | 2017-08-13 13:50:00 |
| A396810   | Raven | 2016-08-22 16:13:00 |
| A410668   | Raven | 2015-11-19 13:41:00 |
| A349996   | Sugar | 2018-01-22 14:32:00 |



## 풀이

- 구해야 할 것  
  - 모든 동물의 아이디와 이름, 보호 시작일을 이름 순으로 조회 
  - 이름이 같은 동물 중에서는 보호를 나중에 시작한 동물을 먼저 보여주기

처음 등장한 이중 조건!

첫번째 조건은 "이름"순이다. ORDER BY에 NAME을 적어주자. 

이름이 같을 경우 보호를 나중에 시작한 동물 : DATETIME이 늦은 동물이 늦게 들어온 동물이겠지?

DATETIME을 역순으로 정렬하면 보호를 나중에 시작한 동물 순이 된다.



생각한 것을 차례대로 적어주자! 

```sql
SELECT ANIMAL_ID, NAME, DATETIME FROM ANIMAL_INS ORDER BY NAME, DATETIME DESC;
```



---



---

## Reference

[[프로그래머스] 여러 기준으로 정렬하기](https://programmers.co.kr/learn/courses/30/lessons/59404)


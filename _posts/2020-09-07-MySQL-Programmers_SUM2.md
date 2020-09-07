---

title:  "[프로그래머스-MySQL] 중복 제거하기 LEVEL 2"
excerpt: "중복 제거하기 문제 풀이, COUNT"
comments: true

categories:
  - Programmers
tags: 
  - [MySQL, Database, Programmers]
toc: true
toc_sticky: true
last_modified_at:  2020-09-07 04:15:00 +0000
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

동물 보호소에 들어온 동물의 이름은 몇 개인지 조회하는 SQL 문을 작성해주세요. 이때 이름이 NULL인 경우는 집계하지 않으며 중복되는 이름은 하나로 칩니다.

##### 예시

예를 들어 `ANIMAL_INS` 테이블이 다음과 같다면

| ANIMAL_ID | ANIMAL_TYPE | DATETIME            | INTAKE_CONDITION | NAME     | SEX_UPON_INTAKE |
| --------- | ----------- | ------------------- | ---------------- | -------- | --------------- |
| A562649   | Dog         | 2014-03-20 18:06:00 | Sick             | NULL     | Spayed Female   |
| A412626   | Dog         | 2016-03-13 11:17:00 | Normal           | *Sam     | Neutered Male   |
| A563492   | Dog         | 2014-10-24 14:45:00 | Normal           | *Sam     | Neutered Male   |
| A513956   | Dog         | 2017-06-14 11:54:00 | Normal           | *Sweetie | Spayed Female   |

보호소에 들어온 동물의 이름은 NULL(없음), `*Sam`, `*Sam`, `*Sweetie`입니다. 이 중 NULL과 중복되는 이름을 고려하면, 보호소에 들어온 동물 이름의 수는 2입니다. 따라서 SQL문을 실행하면 다음과 같이 나와야 합니다.

| count |
| ----- |
| 2     |

※ 컬럼 이름(위 예제에서는 count)은 일치하지 않아도 됩니다.

---

## 풀이

- 구해야 할 것  
  - 동물 보호소에 들어온 동물의 이름은 몇 개인가.
  - 이름이 NULL인 경우는 집계하지 않으며 중복되는 이름은 하나로 친다.

1. 우선 NAME의 갯수를 구해야 하므로 COUNT(NAME) 까지 완성

2. 중복되는 이름은 하나로 친다 = DISTINCT 

3. 이름이 NULL인 경우 집계 X 

   -> COUNT는 원래 NULL인경우 포함하지 않는다. COUNT 활용하라고 만든 문제여서 조건이 들어간 것 같다.

```sql
SELECT COUNT(DISTINCT NAME) FROM ANIMAL_INS 
WHERE NAME IS NOT NULL;
```

```sql
SELECT COUNT(DISTINCT NAME) FROM ANIMAL_INS;
```

---

## Reference

[[프로그래머스] 중복 제거하기](https://programmers.co.kr/learn/courses/30/lessons/59408)


---

title:  "[프로그래머스-MySQL] 고양이와 개는 몇 마리 있을까 LEVEL 2"
excerpt: "고양이와 개는 몇 마리 있을까 문제 풀이, GROUP BY"
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

동물 보호소에 들어온 동물 중 고양이와 개가 각각 몇 마리인지 조회하는 SQL문을 작성해주세요. 이때 고양이를 개보다 먼저 조회해주세요.

##### 예시

예를 들어 `ANIMAL_INS` 테이블이 다음과 같다면

| ANIMAL_ID | ANIMAL_TYPE | DATETIME            | INTAKE_CONDITION | NAME | SEX_UPON_INTAKE |
| --------- | ----------- | ------------------- | ---------------- | ---- | --------------- |
| A373219   | Cat         | 2014-07-29 11:43:00 | Normal           | Ella | Spayed Female   |
| A377750   | Dog         | 2017-10-25 17:17:00 | Normal           | Lucy | Spayed Female   |
| A354540   | Cat         | 2014-12-11 11:48:00 | Normal           | Tux  | Neutered Male   |

고양이는 2마리, 개는 1마리 들어왔습니다. 따라서 SQL문을 실행하면 다음과 같이 나와야 합니다.

| ANIMAL_TYPE | count |
| ----------- | ----- |
| Cat         | 2     |
| Dog         | 1     |

---

## 풀이

- 구해야 할 것  
  - 고양이와 개가 각각 몇 마리일까
  - 고양이를 개보다 먼저 조회할 것 (Cat, Dog 순) = 오름차순 

ANIMAL_TYPE을 GROUP 으로 묶어 COUNT세는 문제!

```sql
SELECT ANIMAL_TYPE, COUNT(ANIMAL_TYPE) AS count 
FROM ANIMAL_INS 
GROUP BY ANIMAL_TYPE
ORDER BY ANIMAL_TYPE;
```



---

## Reference

[[프로그래머스] 고양이와 개는 몇 마리 있을까](https://programmers.co.kr/learn/courses/30/lessons/59040)


---

title:  "[프로그래머스-MySQL] 동물 수 구하기 LEVEL 2"
excerpt: "동물 수 구하기 문제 풀이, COUNT"
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

동물 보호소에 동물이 몇 마리 들어왔는지 조회하는 SQL 문을 작성해주세요.

##### 예시

예를 들어 `ANIMAL_INS` 테이블이 다음과 같다면

| ANIMAL_ID | ANIMAL_TYPE | DATETIME            | INTAKE_CONDITION | NAME     | SEX_UPON_INTAKE |
| --------- | ----------- | ------------------- | ---------------- | -------- | --------------- |
| A399552   | Dog         | 2013-10-14 15:38:00 | Normal           | Jack     | Neutered Male   |
| A379998   | Dog         | 2013-10-23 11:42:00 | Normal           | Disciple | Intact Male     |
| A370852   | Dog         | 2013-11-03 15:04:00 | Normal           | Katie    | Spayed Female   |
| A403564   | Dog         | 2013-11-18 17:03:00 | Normal           | Anna     | Spayed Female   |

동물 보호소에 들어온 동물은 4마리입니다. 따라서 SQL문을 실행하면 다음과 같이 나와야 합니다.

| count |
| ----- |
| 4     |

※ 컬럼 이름(위 예제에서는 count)은 일치하지 않아도 됩니다.

---

## 풀이

- 구해야 할 것  
  - 동물 보호소에 동물이 몇 마리 들어왔는가

데이터가 총 몇 개 인지 확인해주면 된다.  

여기서 ID는 NULL이 될 수 없기 때문에 ID로 COUNT가 가능하다.

단 NAME과 같은 경우, NULL이 들어간 NAME은 COUNT하지않으므로 틀렸습니다가 뜬다.

불안하면 *로 COUNT 해버리자!

```sql
SELECT COUNT(ANIMAL_ID) FROM ANIMAL_INS;
```

```sql
SELECT COUNT(*) FROM ANIMAL_INS; 
```

---

## Reference

[[프로그래머스] 동물 수 구하기](https://programmers.co.kr/learn/courses/30/lessons/59406)


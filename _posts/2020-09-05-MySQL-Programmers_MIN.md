---

title:  "[프로그래머스-MySQL] 최솟값 구하기 LEVEL 2"
excerpt: "최솟값 구하기 문제 풀이, MIN"
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

동물 보호소에 가장 먼저 들어온 동물은 언제 들어왔는지 조회하는 SQL 문을 작성해주세요.

##### 예시

예를 들어 `ANIMAL_INS` 테이블이 다음과 같다면

| ANIMAL_ID | ANIMAL_TYPE | DATETIME            | INTAKE_CONDITION | NAME     | SEX_UPON_INTAKE |
| --------- | ----------- | ------------------- | ---------------- | -------- | --------------- |
| A399552   | Dog         | 2013-10-14 15:38:00 | Normal           | Jack     | Neutered Male   |
| A379998   | Dog         | 2013-10-23 11:42:00 | Normal           | Disciple | Intact Male     |
| A370852   | Dog         | 2013-11-03 15:04:00 | Normal           | Katie    | Spayed Female   |
| A403564   | Dog         | 2013-11-18 17:03:00 | Normal           | Anna     | Spayed Female   |

가장 먼저 들어온 동물은 Jack이고, Jack은 2013-10-14 15:38:00에 들어왔습니다. 따라서 SQL문을 실행하면 다음과 같이 나와야 합니다.

| 시간                |
| ------------------- |
| 2013-10-14 15:38:00 |

---

## 풀이

- 구해야 할 것  
  - 가장 먼저 들어온 동물은 언제 들어왔는가

이 문제에도 두가지 방법이 존재한다.

1. 가장 먼저니까 ORDER BY ASC 로 정렬한 후 제일 위에있는 데이터 값을 출력한다.
2. DATETIME 중 MIN 값을 찾아 출력한다.



생각한 것을 차례대로 적어주자! 

```sql
SELECT DATETIME FROM ANIMAL_INS ORDER BY DATETIME LIMIT 1;
```

```sql
SELECT MIN(DATETIME) FROM ANIMAL_INS; 
```



cf.)  문제 제목이 최솟값 구하기므로 MIN을 활용해서 푸는게 모범답안!



---

## Reference

[[프로그래머스] 최솟값 구하기](https://programmers.co.kr/learn/courses/30/lessons/59038)


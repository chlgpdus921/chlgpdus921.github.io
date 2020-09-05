---

title:  "[프로그래머스-MySQL] 상위 n개 레코드 LEVEL 1"
excerpt: "상위 n개 레코드 문제 풀이, SELECT"
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

동물 보호소에 가장 먼저 들어온 동물의 이름을 조회하는 SQL 문을 작성해주세요.

##### 예시

예를 들어 `ANIMAL_INS` 테이블이 다음과 같다면

| ANIMAL_ID | ANIMAL_TYPE | DATETIME            | INTAKE_CONDITION | NAME     | SEX_UPON_INTAKE |
| --------- | ----------- | ------------------- | ---------------- | -------- | --------------- |
| A399552   | Dog         | 2013-10-14 15:38:00 | Normal           | Jack     | Neutered Male   |
| A379998   | Dog         | 2013-10-23 11:42:00 | Normal           | Disciple | Intact Male     |
| A370852   | Dog         | 2013-11-03 15:04:00 | Normal           | Katie    | Spayed Female   |
| A403564   | Dog         | 2013-11-18 17:03:00 | Normal           | Anna     | Spayed Female   |

이 중 가장 보호소에 먼저 들어온 동물은 Jack입니다. 따라서 SQL문을 실행하면 다음과 같이 나와야 합니다.

| NAME |
| ---- |
| Jack |

※ 보호소에 가장 먼저 들어온 동물은 한 마리인 경우만 테스트 케이스로 주어집니다.

---

## 풀이

- 구해야 할 것  
  - 동물 보호소에 가장 먼저 들어온 동물의 이름을 조회

동물 보호소에 가장 먼저 들어왔다는 것은 DATETIME이 가장 작은 동물이다. 

여기서 우리는 두가지 방법을 생각할 수 있다.

1. DATETIME이 가장 MIN (최소) 인 값을 구하기
2. DATETIME을 ORDER BY로 정렬 후 1번째 줄 출력



생각한 것을 차례대로 적어주자! 

```sql
SELECT NAME FROM ANIMAL_INS WHERE DATETIME = (SELECT MIN(DATETIME) FROM ANIMAL_INS);
```

여기서 LIMIT 설명

- LIMIT 1 : 맨 위에 있는 1개 보여준다.
- LIMIT 3 : 맨 위에서부터 3개까지 보여준다.
- LIMIT 2, 5 : 맨 위에서 2번째부터 5번째까지 보여준다.

```sql
SELECT NAME FROM ANIMAL_INS ORDER BY DATETIME LIMIT 1;
```



cf.) 문제에서는 다행히 상위 1개 레코드 출력이었지만 문제 이름이 상위N개 레코드이므로 LIMIT을 써서 푸는 문제라고 생각한다. 



---

## Reference

[[프로그래머스] 여러 기준으로 정렬하기](https://programmers.co.kr/learn/courses/30/lessons/59404)


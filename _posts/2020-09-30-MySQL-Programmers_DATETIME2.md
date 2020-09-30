---


title:  "[프로그래머스-MySQL] DATETIME에서 DATE로 형 변환 LEVEL 2"
excerpt: "DATETIME에서 DATE로 형 변환, DATETIME"
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

`ANIMAL_INS` 테이블에 등록된 모든 레코드에 대해, 각 동물의 아이디와 이름, 들어온 날짜를 조회하는 SQL문을 작성해주세요. 이때 결과는 아이디 순으로 조회해야 합니다. 시각(시-분-초)을 제외한 날짜(년-월-일)만 보여주세요.

##### 예시

예를 들어, `ANIMAL_INS` 테이블이 다음과 같다면

```
ANIMAL_INS
```

| ANIMAL_ID | ANIMAL_TYPE | DATETIME            | INTAKE_CONDITION | NAME   | SEX_UPON_INTAKE |
| --------- | ----------- | ------------------- | ---------------- | ------ | --------------- |
| A349996   | Cat         | 2018-01-22 14:32:00 | Normal           | Sugar  | Neutered Male   |
| A350276   | Cat         | 2017-08-13 13:50:00 | Normal           | Jewel  | Spayed Female   |
| A350375   | Cat         | 2017-03-06 15:01:00 | Normal           | Meo    | Neutered Male   |
| A352555   | Dog         | 2014-08-08 04:20:00 | Normal           | Harley | Spayed Female   |
| A352713   | Cat         | 2017-04-13 16:29:00 | Normal           | Gia    | Spayed Female   |

SQL문을 실행하면 다음과 같이 나와야 합니다.

| ANIMAL_ID | NAME   | 날짜       |
| --------- | ------ | ---------- |
| A349996   | Sugar  | 2018-01-22 |
| A350276   | Jewel  | 2017-08-13 |
| A350375   | Meo    | 2017-03-06 |
| A352555   | Harley | 2014-08-08 |
| A352713   | Gia    | 2017-04-13 |

---

## 풀이

- 구해야 할 것  
  -   각 동물의 아이디와 이름, 들어온 날짜를 조회
  -   결과는 아이디 순으로 조회
  -   시각(시-분-초)을 제외한 날짜(년-월-일)만 보여주기

| **구분기호** | **역할**                             | **구분기호** | **역할**                           |
| ------------ | ------------------------------------ | ------------ | ---------------------------------- |
| %Y           | 4자리 년도 (2000,1997)               | %m           | 숫자 월 ( 두자리 ) (09,08,12)      |
| %y           | 2자리 년도 (87,97)                   | %c           | 숫자 월(한자리는 한자리)  (1,2)    |
| %M           | 긴 월(영문)  (Janeary, December)     | %d           | 일자 (두자리)  (09,05)             |
| %b           | 짧은 월(영문)  (Jan, Dec, ...)       | %e           | 일자(한자리는 한자리)  (5,9)       |
| %W           | 긴 요일 이름(영문)  (Sunday, Monday) | %I           | 시간 (12시간)  (01, 02, 12)        |
| %a           | 짧은 요일 이름(영문)  (Sun, Tue)     | %H           | 시간(24시간)  (00, 01, 02, 13, 24) |
| %i           | 분 00, 01, 30)                       | %r           | hh:mm:ss AM,PM                     |
| %T           | hh:mm:SS                             | %S           | 초                                 |

```sql
SELECT ANIMAL_ID, NAME, date_format(DATETIME, "%Y-%m-%d") AS "날짜"
FROM ANIMAL_INS 
ORDER BY ANIMAL_ID;
```

---

## Reference

[https://devjhs.tistory.com/89](https://devjhs.tistory.com/89)


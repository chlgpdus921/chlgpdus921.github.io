---

title:  "[프로그래머스-MySQL] 없어진 기록 찾기 LEVEL 3"
excerpt: "없어진 기록 찾기 문제 풀이, JOIN"
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

천재지변으로 인해 일부 데이터가 유실되었습니다. 입양을 간 기록은 있는데, 보호소에 들어온 기록이 없는 동물의 ID와 이름을 ID 순으로 조회하는 SQL문을 작성해주세요.

##### 예시

예를 들어, `ANIMAL_INS` 테이블과 `ANIMAL_OUTS` 테이블이 다음과 같다면

```
ANIMAL_INS
```

| ANIMAL_ID | ANIMAL_TYPE | DATETIME            | INTAKE_CONDITION | NAME | SEX_UPON_INTAKE |
| --------- | ----------- | ------------------- | ---------------- | ---- | --------------- |
| A352713   | Cat         | 2017-04-13 16:29:00 | Normal           | Gia  | Spayed Female   |
| A350375   | Cat         | 2017-03-06 15:01:00 | Normal           | Meo  | Neutered Male   |

```
ANIMAL_OUTS
```

| ANIMAL_ID | ANIMAL_TYPE | DATETIME            | NAME  | SEX_UPON_OUTCOME |
| --------- | ----------- | ------------------- | ----- | ---------------- |
| A349733   | Dog         | 2017-09-27 19:09:00 | Allie | Spayed Female    |
| A352713   | Cat         | 2017-04-25 12:25:00 | Gia   | Spayed Female    |
| A349990   | Cat         | 2018-02-02 14:18:00 | Spice | Spayed Female    |

`ANIMAL_OUTS` 테이블에서

- Allie의 ID는 `ANIMAL_INS`에 없으므로, Allie의 데이터는 유실되었습니다.
- Gia의 ID는 `ANIMAL_INS`에 있으므로, Gia의 데이터는 유실되지 않았습니다.
- Spice의 ID는 `ANIMAL_INS`에 없으므로, Spice의 데이터는 유실되었습니다.

따라서 SQL문을 실행하면 다음과 같이 나와야 합니다.

| ANIMAL_ID | NAME  |
| --------- | ----- |
| A349733   | Allie |
| A349990   | Spice |



## 풀이

- 구해야 할 것  
  -  입양을 간 기록은 있는데, 보호소에 들어온 기록이 없는 동물의 ID와 이름
  -  ID 순으로 조회 (= ORDER BY ANIMAL_ID)

[[MySQL] Join (Outer Join, Inner Join) 설명 및 예제](https://chlgpdus921.github.io/mysql/MySQL-JOIN/)   <---- 문제를 풀기 전 다음 글을 읽고오자.

테이블이 2개나 생겼다. 내용을 정리해보자. ( JOIN문제는 글로 정리하고 그림 그리는게 쉽다.)

1. ANIMAL_INS : 동물 보호소에 들어온 동물의 정보
2. ANIMAL_OUTS : 동물 보호소에서 입양 보낸 동물의 정보

입양을 갔다 = ANIMAL_OUTS 테이블에 정보가 있다.

보호소에 들어온 기록이 없다 = ANIMAL_INS 테이블에 정보가 없다.

- **즉 ANIMAL_OUTS  (B) 에는 있지만 ANIMAL_INS (A) 에는 없는 정보**

  <img src="https://user-images.githubusercontent.com/32683894/91834237-b97b7180-ec82-11ea-816d-54e44706ae49.png" alt="image" style="zoom:50%;" />

  다음과 같은 그림을 생각할 수있다.

  오른쪽에 색칠되어 있으니 RIGHT JOIN

  그러나 순수 B를 구해야 하므로 A.KEY  IS NULL을 넣어줄 것 (이 문제에서 KEY는 ID겠지?)

  (이해가 안된다면 첨부된 링크를 보고 형식을 이해하고 오자!)

```sql
SELECT B.ANIMAL_ID, B.NAME 
FROM ANIMAL_INS A RIGHT JOIN ANIMAL_OUTS B ON A.ANIMAL_ID = B.ANIMAL_ID 
WHERE A.ANIMAL_ID IS NULL
ORDER BY B.ANIMAL_ID;
```

---

## Reference

[[프로그래머스] 없어진 기록 찾기](https://programmers.co.kr/learn/courses/30/lessons/59042)

[[MySQL] Join (Outer Join, Inner Join) 설명 및 예제](https://chlgpdus921.github.io/mysql/MySQL-JOIN/)


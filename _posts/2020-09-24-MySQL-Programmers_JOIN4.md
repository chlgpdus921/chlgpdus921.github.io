---


title:  "[프로그래머스-MySQL] 보호소에서 중성화한 동물 LEVEL 4"
excerpt: "보호소에서 중성화한 동물 문제 풀이, JOIN"
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

보호소에서 중성화 수술을 거친 동물 정보를 알아보려 합니다. 보호소에 들어올 당시에는 중성화되지 않았지만, 보호소를 나갈 당시에는 중성화된 동물의 아이디와 생물 종, 이름을 조회하는 아이디 순으로 조회하는 SQL 문을 작성해주세요.

(중성화 : 중성화를 거치지 않은 동물은 `성별 및 중성화 여부`에 Intact, 중성화를 거친 동물은 `Spayed` 또는 `Neutered`라고 표시되어있습니다. )

##### 예시

예를 들어, `ANIMAL_INS` 테이블과 `ANIMAL_OUTS` 테이블이 다음과 같다면

```
ANIMAL_INS
```

| ANIMAL_ID | ANIMAL_TYPE | DATETIME            | INTAKE_CONDITION | NAME      | SEX_UPON_INTAKE |
| --------- | ----------- | ------------------- | ---------------- | --------- | --------------- |
| A367438   | Dog         | 2015-09-10 16:01:00 | Normal           | Cookie    | Spayed Female   |
| A382192   | Dog         | 2015-03-13 13:14:00 | Normal           | Maxwell 2 | Intact Male     |
| A405494   | Dog         | 2014-05-16 14:17:00 | Normal           | Kaila     | Spayed Female   |
| A410330   | Dog         | 2016-09-11 14:09:00 | Sick             | Chewy     | Intact Female   |

```
ANIMAL_OUTS
```

| ANIMAL_ID | ANIMAL_TYPE | DATETIME            | NAME      | SEX_UPON_OUTCOME |
| --------- | ----------- | ------------------- | --------- | ---------------- |
| A367438   | Dog         | 2015-09-12 13:30:00 | Cookie    | Spayed Female    |
| A382192   | Dog         | 2015-03-16 13:46:00 | Maxwell 2 | Neutered Male    |
| A405494   | Dog         | 2014-05-20 11:44:00 | Kaila     | Spayed Female    |
| A410330   | Dog         | 2016-09-13 13:46:00 | Chewy     | Spayed Female    |

- Cookie는 보호소에 들어올 당시에 이미 중성화되어있었습니다.
- Maxwell 2는 보호소에 들어온 후 중성화되었습니다.
- Kaila는 보호소에 들어올 당시에 이미 중성화되어있었습니다.
- Chewy는 보호소에 들어온 후 중성화되었습니다.

따라서 SQL문을 실행하면 다음과 같이 나와야 합니다.

| ANIMAL_ID | ANIMAL_TYPE | NAME      |
| --------- | ----------- | --------- |
| A382192   | Dog         | Maxwell 2 |
| A410330   | Dog         | Chewy     |

## 풀이

- 구해야 할 것  
  -   보호소에 들어올 당시에는 중성화되지 않았지만, 보호소를 나갈 당시에는 중성화된 동물의 아이디와 생물 종, 이름을 조회
      -   중성화를 거치지 않은 동물 SEX_UPON_INTAKE =  Intact 
      -   중성화를 거친 동물은 SEX_UPON_OUTCOME =  Spayed OR Neutered 
  -   아이디 순으로 조회

[[MySQL] Join (Outer Join, Inner Join) 설명 및 예제](https://chlgpdus921.github.io/mysql/MySQL-JOIN/)   <---- 문제를 풀기 전 다음 글을 읽고 오자.



테이블이 2개나 생겼다. 내용을 정리해보자. ( JOIN문제는 글로 정리하고 그림 그리는게 쉽다.)

1. ANIMAL_INS : 동물 보호소에 들어온 동물의 정보
2. ANIMAL_OUTS : 동물 보호소에서 입양 보낸 동물의 정보

보호소에 들어올 당시에는 중성화X  = ANIMAL_INS  테이블 정보

보호소를 나갈 당시에는 중성화O  = ANIMAL_OUTS 테이블 정보

- 즉, ANIMAL_INS (A) 에서는 Intact고, ANIMAL_OUTS (B) 에서는 Spayed OR Neutered 
- 보호소에 있다가 입양됐으니, A와 B 둘 TABLE에 존재하는 정보 (= INNER JOIN)



<img src="https://user-images.githubusercontent.com/32683894/91835533-7de1a700-ec84-11ea-9435-2d0c66b2ed5d.png" alt="image" style="zoom:50%;" />

다음과 같은 그림을 생각할 수있다.

- 보호소에 들어올 당시에는 중성화X  = ANIMAL_INS  테이블 정보 = Intact
- 보호소를 나갈 당시에는 중성화O  = ANIMAL_OUTS 테이블 정보 = Spayed OR Neutered 

(이해가 안된다면 첨부된 링크를 보고 형식을 이해하고 오자!)

```sql
SELECT A.ANIMAL_ID, A.ANIMAL_TYPE, A.NAME 
FROM ANIMAL_INS A INNER JOIN ANIMAL_OUTS B
ON A.ANIMAL_ID = B.ANIMAL_ID
WHERE 
(A.SEX_UPON_INTAKE = "Intact Male" OR A.SEX_UPON_INTAKE = "Intact Female" )
AND (B.SEX_UPON_OUTCOME ="Spayed Male" OR B.SEX_UPON_OUTCOME ="Spayed Female" 
OR  B.SEX_UPON_OUTCOME ="Neutered Male" OR B.SEX_UPON_OUTCOME ="Neutered Female" )
ORDER BY A.ANIMAL_ID;
```

중복이 많은데 줄여쓰는 방법은 없을까? 존재한다 

> LIKE("Intact%") - Intact Male ( O ), Male Intact ( X )
>
> LIKE("%Intact") - Intact Male ( X ), Male Intact ( O )
>
> LIKE("%Intact%") - Intact Male ( O ), Male Intact ( O )

```sql
SELECT A.ANIMAL_ID, A.ANIMAL_TYPE, A.NAME 
FROM ANIMAL_INS A INNER JOIN ANIMAL_OUTS B
ON A.ANIMAL_ID = B.ANIMAL_ID
WHERE 
(A.SEX_UPON_INTAKE LIKE "Intact%") AND 
(B.SEX_UPON_OUTCOME LIKE "Spayed%" OR B.SEX_UPON_OUTCOME LIKE "Neutered%")
ORDER BY A.ANIMAL_ID;
```



---

## Reference

[[프로그래머스] 보호소에서 중성화한 동물](https://programmers.co.kr/learn/courses/30/lessons/59044)

[[MySQL] Join (Outer Join, Inner Join) 설명 및 예제](https://chlgpdus921.github.io/mysql/MySQL-JOIN/)


---

title:  "[프로그래머스-MySQL] 입양 시각 구하기(2) LEVEL 4"
excerpt: "입양 시각 구하기(2) 문제 풀이, GROUP BY"
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

`ANIMAL_OUTS` 테이블은 동물 보호소에서 입양 보낸 동물의 정보를 담은 테이블입니다. `ANIMAL_OUTS` 테이블 구조는 다음과 같으며, `ANIMAL_ID`, `ANIMAL_TYPE`, `DATETIME`, `NAME`, `SEX_UPON_OUTCOME`는 각각 동물의 아이디, 생물 종, 입양일, 이름, 성별 및 중성화 여부를 나타냅니다.

| NAME             | TYPE       | NULLABLE |
| ---------------- | ---------- | -------- |
| ANIMAL_ID        | VARCHAR(N) | FALSE    |
| ANIMAL_TYPE      | VARCHAR(N) | FALSE    |
| DATETIME         | DATETIME   | FALSE    |
| NAME             | VARCHAR(N) | TRUE     |
| SEX_UPON_OUTCOME | VARCHAR(N) | FALSE    |

보호소에서는 몇 시에 입양이 가장 활발하게 일어나는지 알아보려 합니다. 0시부터 23시까지, 각 시간대별로 입양이 몇 건이나 발생했는지 조회하는 SQL문을 작성해주세요. 이때 결과는 시간대 순으로 정렬해야 합니다.

##### 예시

SQL문을 실행하면 다음과 같이 나와야 합니다.

| HOUR | COUNT |
| ---- | ----- |
| 0    | 0     |
| 1    | 0     |
| 2    | 0     |
| 3    | 0     |
| 4    | 0     |
| 5    | 0     |
| 6    | 0     |
| 7    | 3     |
| 8    | 1     |
| 9    | 1     |
| 10   | 2     |
| 11   | 13    |
| 12   | 10    |
| 13   | 14    |
| 14   | 9     |
| 15   | 7     |
| 16   | 10    |
| 17   | 12    |
| 18   | 16    |
| 19   | 2     |
| 20   | 0     |
| 21   | 0     |
| 22   | 0     |
| 23   | 0     |



## 풀이

- 구해야 할 것  
  -  0시부터 23시까지, 각 시간대별로 입양이 몇 건이나 발생했는가
  - 결과는 시간대 순으로 정렬 (=ORDER BY ASC)



LEVEL 4답다! SELECT만 알던 나에게 이 문제는 구글링해서 참고한 후 풀었다.

입양 시각 구하기(1)과 다른 것은 Data에 없는 HOUR까지 프린트 해야한다는 점이다.

이 문제는 쿼리문에서 로컬 변수를 활용해야 한다.

세미콜론 안찍어서 오류가나 고생했다. 잊지 말자

```sql
SET @hour := -1; --변수 선언 (세미콜론!)

SELECT (@hour := @hour +1) AS HOUR, 
(SELECT COUNT(*) FROM ANIMAL_OUTS WHERE HOUR(DATETIME) = @hour) AS COUNT 
FROM ANIMAL_OUTS 
WHERE @hour < 23
ORDER BY @hour;
```





---

## Reference

[[프로그래머스] 입양 시각 구하기(2)](https://programmers.co.kr/learn/courses/30/lessons/59413)


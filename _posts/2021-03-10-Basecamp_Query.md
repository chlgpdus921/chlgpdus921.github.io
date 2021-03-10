---
title:  "테이블 및 쿼리 작성법"
excerpt: "NHN basecamp 기술 교육 내용 회고입니다."
comments: true

categories:
  - basecamp
tags: 
  - [basecamp]
toc: true
toc_sticky: true
last_modified_at:  2021-02-21 03:15:00 +0000
---

## Goal

> - 테이블 및 쿼리 작성법을 이해한다. 
> - 인덱스 생성 및 비용에 대해 이해한다. 
> - NOW() 와 SYSDATE() 차이를 알 수 있다.

---

### 테이블 작성하는 법

- data type 은 최대한 작게 설계하기 

**Char(1)** 

- 'Y', 'N' / 직관적

**Tinyint**

- 0,1 저장 -> 1byte



### NOT NULL 속성 적용

- 기본이 null 허용

- mysql 은 null 허용하면 컬럼당 1byte 를 추가적으로 사용한다. 



### 쿼리 작성하는 법

- Select 절에는 필요한 컬럼만 작성
  - 불필요한 자원 소모
  - select * (x)



## 인덱스 생성 기준

#### **cardinality** :

- 인덱싱 된 컬럼의 유니크한 값의 수 

- show index from 컬럼명;

- 8개의 페이지 샘플링으로 통계된 값. 근사치 확인

- cardinality가 높으면 유니크한 값들이 많다는 뜻



### 결합 인덱스(컬럼 여러개) 생성시 고려 

equal 조건은 좌측, range 조건은 우측 배치



### join절의 on에 해당하는 컬럼에 인덱스 추가 

```mysql
Create index idx_rest on reservation (reservationid);
```



### 인덱스도 비용이다. 

- 테이블과 마찬가지로 공간을 차지 
- insert, update, delete시 인덱스도 변경 필요. 조회는 빠름
- 쿼리 빈도수/ 쿼리 조건절/ 데이터 분포도에 따라 최소한의 인덱스를 생성하기 

```mysql
(int) order_no = '1' 
# 우측에서 형변환. 인덱스 활용 가능

(varchar) order_status_cd = 10; 
# str이라서 좌측에서 형변환. 인덱스 활용 불가

(datetime) order_umdt = '2011-02-17'; 
# 우측에서 형변환. 인덱스 활용 가능

# 결론 : 이런거 따지지말고 똑같이 dateType을 맞춰주자.
```



### LIKE

- 와일드카드가 검색어 앞쪽 -> 인덱스 레인지 스캔 불가
- 웬만하면 like 안쓰는 것이 좋음



### NOW() vs SYSDATE()

```mysql
select SYSDATE(), sleep(2), SYSDATE();
```

- now()는 두번쓰면 동일한 결과.

- sysdate() 는 두번쓰면 다른결과. 
  - sysdate는 안정적으로 복제 불가 (master에 실행된것을 슬레이브에 넘기는데 넘겨주는 데이터가 각각 달라서 날짜의 차이가 발생하게 된다. )
  - Now()쓰는 것을 권장 



### 실행계획 결과 정보 확인 방법

- 쿼리앞에 explain 붙혀주기 
- Explain format = tree (모양 보기편함)





## Reference

교육명 : NHN basecamp SQL 이론 및 쿼리 검수 결과 공유

강사님 성함 : 남준희 선임님

교육 요약 내용입니다. (좋은 교육 감사합니다!)
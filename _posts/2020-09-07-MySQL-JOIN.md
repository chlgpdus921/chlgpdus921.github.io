---

title:  "[MySQL] Join (Outer Join, Inner Join) 설명 및 예제"
excerpt: "MySQL Join 종류 마스터 해보자 (LEFT JOIN, RIGHT JOIN, FULL OUTER JOIN)"
comments: true

categories:
  - MySQL
tags: 
  - [MySQL, Database, join]
toc: true
toc_sticky: true
last_modified_at:  2020-09-01 19:15:00 +0000
---

## Goal

> - Join에 대해 이해하고 이를 활용할 수 있다. 
> - Left Join, Right Join 차이점을 이해한다. 

---

## 한 눈에 보는 전체 사진

![image](https://user-images.githubusercontent.com/32683894/91840106-1d099d00-ec8b-11ea-87d0-248be6b55a46.png)



---

## 1. LEFT JOIN (= LEFT OUTER JOIN)

LEFT OUTER JOIN 이라고도 쓰이고, LEFT JOIN 으로 쓰는 개발자도 있길래 구글링해보니 둘다 똑같은 말이라고 한다. 

<center><img src="https://user-images.githubusercontent.com/32683894/91832062-da8e9300-ec7f-11ea-9c24-b4176ecbfc87.png" alt="image" style="zoom:50%;" /></center>

LEFT JOIN은 A와 B 테이블 중에  **A값 + A와 B의 KEY값이 같은 결과 ** 를 리턴하는 것이다. 

```sql
SELECT * FROM TableA A LEFT JOIN TableB B ON A.key = B.key;
```



---

## 2. RIGHT JOIN (= RIGHT OUTER JOIN)

RIGHT JOIN은 A와 B 테이블 중에 **B 값 + A와 B의 KEY값이 같은 결과** 를 리턴하는 것이다.

<center><img src="https://user-images.githubusercontent.com/32683894/91833819-26dad280-ec82-11ea-9256-18181ddc96a0.png" alt="image" style="zoom:50%;" /></center>

```sql
SELECT * FROM TableA A RIGHT JOIN TableB B ON A.key = B.key;
```



---

## 3. LEFT JOIN (순수 A만 구할 때)

순수 A만 구할 때, 순수 A들은 JOIN 후 B가 가진 테이블 COLUMN들의 항목이 NULL로 포함되어 있을 것이다. 

그래서 B의 KEY 값이 IS NULL인지 확인한다.

<center><img src="https://user-images.githubusercontent.com/32683894/91834764-6eae2980-ec83-11ea-8745-cb69161157d5.png" alt="image" style="zoom:50%;" /></center>

```sql
SELECT * FROM TableA A LEFT JOIN TableB B ON A.key = B.key
WHERE B.Key IS NULL;
```



---

## 4. RIGHT JOIN (순수 B만 구할 때)

순수 B만 구할 때, 순수 B들은 JOIN 후 A가 가진 테이블 COLUMN들의 항목이 NULL로 포함되어 있을 것이다. 

그래서 A의 KEY 값이 IS NULL인지 확인한다.

<center><img src="https://user-images.githubusercontent.com/32683894/91834237-b97b7180-ec82-11ea-816d-54e44706ae49.png" alt="image" style="zoom:50%;" /></center>

```sql
SELECT * FROM TableA A RIGHT JOIN TableB B ON A.key = B.key
WHERE A.Key IS NULL;
```

---

## 5. INNER JOIN (A와 B의 교집합)

드디어 등장한 INNER JOIN 

A와 B의 교집합 ( 서로 중복되는 값)을 보여준다. 

<center><img src="https://user-images.githubusercontent.com/32683894/91835533-7de1a700-ec84-11ea-9435-2d0c66b2ed5d.png" alt="image" style="zoom:50%;" /></center>

```sql
SELECT * FROM TableA A INNER JOIN TableB B ON A.key = B.key;
```

---

## 6. FULL OUTER JOIN

이름에서도 알수있는 FULL의 의미! A와 B 전체를 구하는 것!

<center><img src="https://user-images.githubusercontent.com/32683894/91835803-d87b0300-ec84-11ea-984e-7abea0d1568c.png" alt="image" style="zoom:50%;" /></center>

```sql
SELECT * FROM TableA A FULL OUTER JOIN TableB B ON A.key = B.key;
```



여기서 문제! MySQL은 FULL OUTER JOIN을 지원하지 않는다고 한다.

그래서 LEFT JOIN과 RIGHT JOIN을 UNION해서 사용해야한다.

```mysql
SELECT * FROM TableA A LEFT JOIN TableB B 
UNION
SELECT * FROM TableA A RIGHT JOIN TableB B
```

---

## 7. FULL OUTER JOIN (교집합 제외)

<center><img src="https://user-images.githubusercontent.com/32683894/91838564-ae2b4480-ec88-11ea-93e9-7fc17b8962ca.png" alt="image" style="zoom:50%;" /></center>

```sql
SELECT * FROM TableA A LEFT JOIN TableB B 
UNION
SELECT * FROM TableA A RIGHT JOIN TableB B
WHERE A.key IS NULL OR B.key IS NULL
```



---

## Reference

https://yoo-hyeok.tistory.com/98

그림들은 모두 직접 제작했다. (출처 남기고 퍼가기 가능)


# SQL문제

[toc]

## 프로그래머스_모든레코드조회하기

> [프로그래머스_모든레코드조회하기](https://programmers.co.kr/learn/courses/30/lessons/59034)

```mysql
-- 코드를 입력하세요
SELECT *
FROM ANIMAL_INS
ORDER BY ANIMAL_ID;
```



## 프로그래머스_역순정렬하기

> [프로그래머스_역순정렬하기](https://programmers.co.kr/learn/courses/30/lessons/59035)

```mysql
-- 코드를 입력하세요
SELECT NAME, DATETIME
FROM ANIMAL_INS
ORDER BY ANIMAL_ID DESC;
```



## 프로그래머스_아픈동물찾기

> [프로그래머스_아픈동물찾기](https://programmers.co.kr/learn/courses/30/lessons/59036)

```mysql
-- 코드를 입력하세요
SELECT ANIMAL_ID, NAME
FROM ANIMAL_INS
WHERE INTAKE_CONDITION = "Sick"
ORDER BY ANIMAL_ID;
```



## 프로그래머스_어린동물찾기

> [프로그래머스_어린동물찾기](https://programmers.co.kr/learn/courses/30/lessons/59037)

```mysql
-- 코드를 입력하세요
SELECT ANIMAL_ID, NAME
FROM ANIMAL_INS
WHERE INTAKE_CONDITION != "Aged"
ORDER BY ANIMAL_ID;
```



## 프로그래머스_동물아이디와 이름

> [프로그래머스_동물아이디와이름](https://programmers.co.kr/learn/courses/30/lessons/59403)

```mysql
-- 코드를 입력하세요
SELECT ANIMAL_ID, NAME
FROM ANIMAL_INS
ORDER BY ANIMAL_ID;
```



## 프로그래머스_여러기준으로정렬하기

> [프로그래머스_여러기준으로정렬하기](https://programmers.co.kr/learn/courses/30/lessons/59404)

```mysql
-- 코드를 입력하세요
SELECT ANIMAL_ID, NAME, DATETIME
FROM ANIMAL_INS
ORDER BY NAME, DATETIME DESC;
```



## 프로그래머스_상위N개레코드

> [프로그래머스_상위N개레코드](https://programmers.co.kr/learn/courses/30/lessons/59405)

```mysql
-- 코드를 입력하세요
SELECT NAME
FROM ANIMAL_INS
ORDER BY DATETIME
LIMIT 1;
```



## 프로그래머스_최댓값구하기

>[프로그래머스_최댓값구하기](https://programmers.co.kr/learn/courses/30/lessons/59415#)

```mysql
-- 코드를 입력하세요
SELECT MAX(DATETIME) FROM ANIMAL_INS;
```



## 프로그래머스_최솟값구하기

> [프로그래머스_최솟값구하기](https://programmers.co.kr/learn/courses/30/lessons/59038)

```mysql
-- 코드를 입력하세요
SELECT MIN(DATETIME) FROM ANIMAL_INS;
```



## 프로그래머스_동물수구하기

> [프로그래머스_동물수구하기](https://programmers.co.kr/learn/courses/30/lessons/59406)

```mysql
-- 코드를 입력하세요
SELECT COUNT(*) FROM ANIMAL_INS;
```



## 프로그래머스_중복제거하기

> [프로그래머스_중복제거하기](https://programmers.co.kr/learn/courses/30/lessons/59408)
>
> count 함수는 Null을 세지 않기 떄문에 굳이 WHERE NAME IS NOT NULL을 쓰지 않았습니다.

```mysql
-- 코드를 입력하세요
SELECT COUNT(DISTINCT NAME) AS count
FROM ANIMAL_INS;
```



## 프로그래머스_고양이와 개는 몇마리 있을까

> [프로그래머스_고양이와 개는 몇마리 있을까](https://programmers.co.kr/learn/courses/30/lessons/59040)

```mysql
-- 코드를 입력하세요
SELECT ANIMAL_TYPE, COUNT(ANIMAL_ID) AS count
FROM ANIMAL_INS
WHERE ANIMAL_TYPE IN ("Cat","Dog")
GROUP BY ANIMAL_TYPE
ORDER BY ANIMAL_TYPE;
```



## 프로그래머스_동명 동물 수 찾기

> [프로그래머스_동명 동물 수 찾기](https://programmers.co.kr/learn/courses/30/lessons/59041)

```mysql
-- 코드를 입력하세요
SELECT NAME, COUNT(ANIMAL_ID) AS COUNT
FROM ANIMAL_INS
GROUP BY NAME
HAVING COUNT(NAME) > 1
ORDER BY NAME;
```



## 프로그래머스_입양시각구하기(1)

> [프로그래머스_입양시각구하기(1)](https://programmers.co.kr/learn/courses/30/lessons/59412)
>
> #### GROUP BY 절
>
> GROUP BY 절은 선택된 레코드의 집합을 필드의 값이나 표현식에 의해 그룹화한 결과 집합을 반환
>
> 즉, GROUP BY 절은 하나의 그룹을 하나의 레코드로 반환하므로, 결과 집합의 크기를 줄여주는 역할
>
> #### HAVING 절
>
> HAVING 절은 SELECT 문의 WHERE 절처럼 GROUP BY 절에 의해 반환되는 결과 집합의 조건을 설정

```mysql
-- 코드를 입력하세요
SELECT HOUR(DATETIME) AS HOUR, COUNT(ANIMAL_ID) AS COUNT
FROM ANIMAL_OUTS
WHERE DATE_FORMAT(DATETIME,"%H:%i") BETWEEN "09:00" AND "19:59"
GROUP BY HOUR(DATETIME)
ORDER BY HOUR(DATETIME);

-- 코드를 입력하세요
SELECT HOUR(DATETIME) AS HOUR, COUNT(DATETIME) AS COUNT
FROM ANIMAL_OUTS
GROUP BY HOUR
HAVING HOUR BETWEEN "9" AND "19"
ORDER BY HOUR;
```

- 다른코드

```mysql
-- 코드를 입력하세요
SELECT HOUR(DATETIME) AS HOUR, COUNT(DATETIME) AS COUNT
FROM ANIMAL_OUTS
GROUP BY HOUR
HAVING HOUR BETWEEN 9 AND 19
ORDER BY HOUR

-- 코드를 입력하세요
select date_format(datetime, '%H') as 'HOUR', count('HOUR') as count
from animal_outs
group by HOUR
having HOUR between 9 and 20
order by HOUR
```



## 프로그래머스_입양시각구하기(2)

> [프로그래머스_입양시각구하기(2)](https://programmers.co.kr/learn/courses/30/lessons/59413)
>
> `WITH RECURSIVE`  함수
>
> 1) 메모리상에 가상의 테이블을 저장
>
> 2) 재귀 쿼리를 이용하여 실제로 테이블을 생성하거나 데이터삽입(INSERT)을 하지 않아도 가상 테이블을 생성할 수 있다.
>
> ```mysql
> WITH RECURSIVE 테이블명 AS(
> SELECT 초기값 AS 컬럼별명1
> UNION ALL
> SELECT 컬럼별명1 계산식 FROM 테이블명 WHERE 제어문)
> ```
>
> 예시 : H(칼럼)이 초기값 1부터 제어문에 합당하는 5까지의 데이터를 갖는 가상 테이블 생성
>
> ```mysql
> WITH RECURSIVE TABLENAME AS(
> SELECT 1 AS H
> UNION ALL
> SELECT H+1 FROM TABLENAME WHERE H<5)
> 
> SELECT * FROM TABLENAME;
> ```
>
> 결과
>
> | H    |
> | ---- |
> | 1    |
> | 2    |
> | 3    |
> | 4    |
> | 5    |
>
> #### UNION
>
> UNION은 여러 개의 SELECT 문의 결과를 하나의 테이블이나 결과 집합으로 표현할 때 사용
>
> 이때 각각의 SELECT 문으로 선택된 필드의 개수와 타입은 모두 같아야 하며, 필드의 순서 또한 같아야함
>
> #### UNION ALL
>
> 위의 예제처럼 UNION은 DISTINCT 키워드를 따로 명시하지 않아도 기본적으로 중복되는 레코드를 제거됨.
>
> 따라서 중복되는 레코드까지 모두 출력하고 싶다면, ALL 키워드를 사용

```mysql
-- 코드를 입력하세요
WITH RECURSIVE TIME AS(
SELECT 0 AS H
UNION ALL
SELECT H+1 FROM TIME WHERE H<23)

SELECT H AS HOUR, COUNT(DATETIME) AS COUNT
FROM TIME
LEFT JOIN ANIMAL_OUTS
ON H = HOUR(DATETIME)
GROUP BY H
ORDER BY H;
```



## 프로그래머스_이름이없는동물의아이디

> [프로그래머스_이름이없는동물의아이디](https://programmers.co.kr/learn/courses/30/lessons/59039)

``` mysql
-- 코드를 입력하세요
SELECT ANIMAL_ID
FROM ANIMAL_INS
WHERE NAME IS NULL
ORDER BY ANIMAL_ID;
```



## 프로그래머스_이름이있는동물의아이디

> [프로그래머스_이름이있는동물의아이디](https://programmers.co.kr/learn/courses/30/lessons/59047)

``` mysql
-- 코드를 입력하세요
SELECT ANIMAL_ID
FROM ANIMAL_INS
WHERE NAME IS NOT NULL
ORDER BY ANIMAL_ID;
```



## 프로그래머스_NULL처리하기

> [프로그래머스_NULL처리하기](https://programmers.co.kr/learn/courses/30/lessons/59410)

``` mysql
-- 코드를 입력하세요
SELECT ANIMAL_TYPE, IFNULL(NAME,"No name") AS NAME, SEX_UPON_INTAKE
FROM ANIMAL_INS
ORDER BY ANIMAL_ID;
```



## 프로그래머스_없어진기록찾기

> [프로그래머스_없어진기록찾기](https://programmers.co.kr/learn/courses/30/lessons/59042)
>
> **USING VS ON 차이**
>
> USING은 두 테이블간 필드이름이 같을 경우 사용
>
> ON은 만일 조인시 칼럼 이름이 다를경우, 같아도 상용가능

```mysql
-- 코드를 입력하세요
SELECT O.ANIMAL_ID, O.NAME
FROM ANIMAL_OUTS AS O
LEFT JOIN ANIMAL_INS AS I USING(ANIMAL_ID)
WHERE I.ANIMAL_ID IS NULL
ORDER BY O.ANIMAL_ID;
```



## 프로그래머스_있었는데요없었습니다

> [프로그래머스_있었는데요없었습니다](https://programmers.co.kr/learn/courses/30/lessons/59043)

```mysql
-- 코드를 입력하세요
SELECT I.ANIMAL_ID, I.NAME
FROM ANIMAL_INS AS I
JOIN ANIMAL_OUTS AS O
USING(ANIMAL_ID)
WHERE O.DATETIME < I.DATETIME
ORDER BY I.DATETIME;
```



## 프로그래머스_오랜기간보호한동물(1)

> [프로그래머스_오랜기간보호한동물(1)](https://programmers.co.kr/learn/courses/30/lessons/59044)

```mysql
-- 코드를 입력하세요
SELECT I.NAME, I.DATETIME
FROM ANIMAL_INS AS I
LEFT JOIN ANIMAL_OUTS AS O
USING(ANIMAL_ID)
WHERE O.ANIMAL_ID IS NULL
ORDER BY I.DATETIME
LIMIT 3;

-- 코드를 입력하세요
SELECT I.NAME, I.DATETIME
FROM ANIMAL_INS AS I
LEFT OUTER JOIN ANIMAL_OUTS AS O
USING(ANIMAL_ID)
WHERE O.ANIMAL_ID IS NULL
ORDER BY I.DATETIME
LIMIT 3;

```

- 다른코드

```mysql
SELECT AI.NAME, AI.DATETIME
FROM ANIMAL_INS AS AI
LEFT OUTER JOIN
ANIMAL_OUTS AS AO
USING (ANIMAL_ID)
WHERE AO.ANIMAL_ID IS NULL
ORDER BY AI.DATETIME
LIMIT 3
```



## 프로그래머스_보호소에서 중성화한 동물

> [프로그래머스_보호소에서 중성화한 동물](https://programmers.co.kr/learn/courses/30/lessons/59045)

```mysql
-- 코드를 입력하세요
SELECT I.ANIMAL_ID, I.ANIMAL_TYPE, I.NAME
FROM ANIMAL_INS AS I
JOIN ANIMAL_OUTS AS O
USING(ANIMAL_ID)
WHERE I.SEX_UPON_INTAKE != O.SEX_UPON_OUTCOME
ORDER BY O.ANIMAL_ID;

-- 코드를 입력하세요
SELECT O.ANIMAL_ID, O.ANIMAL_TYPE, O.NAME
FROM ANIMAL_OUTS AS O
LEFT OUTER JOIN ANIMAL_INS AS I
USING(ANIMAL_ID)
WHERE O.SEX_UPON_OUTCOME != I.SEX_UPON_INTAKE
ORDER BY O.ANIMAL_ID;
```

- 다른코드

> OUTER JOIN에선 LEFT, RIGHT 말고도 추가로 FULL OUTER JOIN도 존재한다. 다만 MySQL에선 FULL OUTER JOIN이 지원이 되지 않기에 INNER JOIN과 OUTER JOIN을 활용해서 만들어야 한다.
>
> **JOIN의 처리에서 어느 테이블을 먼저 읽을지를 결정하는 것은 상당히 중요하다.** 처리할 작업량에 따라 속도가 달라지기 때문이다. **INNER JOIN은** 어느 테이블을 먼저 읽어도 결과가 달라지지 않기에 **MySQL Optimizer가 JOIN의 순서를 조절해서 다양한 방법으로 최적화를 수행할 수 있다.** 그러나 **OUTER JOIN**은 반드시 **OUTER가 되는 테이블을 먼저 읽어야 하기 때문에 JOIN 순서를 Optimizer가 선택할 수 없다.**
>
> #### [**OUTER JOIN**](https://aridom.tistory.com/50)
>
> **INNER JOIN**에선 INNER Table에 일치하는 레코드가 있으면 가져오고, **일치하는게 없으면 버리는 걸 알 수 있다**. 이와 다르게 **OUTER JOIN**에선 INNER Table에 **일치하는 레코드가 없으면 모두 NULL로 채워서 가져온다**. 즉, INNER JOIN에서는 일치하는 레코드를 찾지 못했을 때는 OUTER Table의 결과를 모두 버렸지만 **OUTER JOIN에서는 OUTER Table의 결과를 버리지 않고 남겨준다.**
>
> **이 또한 Outer Table에서 만족하는 레코드 개수가 적을수록 속도가 빨라지는 특징을 가진다.**

```mysql
-- 코드를 입력하세요
SELECT O.ANIMAL_ID, O.ANIMAL_TYPE, O.NAME
FROM ANIMAL_OUTS AS O
LEFT OUTER JOIN ANIMAL_INS AS I
ON O.ANIMAL_ID = I.ANIMAL_ID
WHERE O.SEX_UPON_OUTCOME != I.SEX_UPON_INTAKE
ORDER BY ANIMAL_ID
```



## 프로그래머스_루시와엘라찾기

> [프로그래머스_루시와엘라찾기](https://programmers.co.kr/learn/courses/30/lessons/59046)

```mysql
-- 코드를 입력하세요
SELECT ANIMAL_ID, NAME, SEX_UPON_INTAKE
FROM ANIMAL_INS
WHERE NAME IN ("Lucy", "Ella", "Pickle", "Rogan", "Sabrina", "Mitty")
ORDER BY ANIMAL_ID;
```



## 프로그래머스_이름에 EL이 들어가는 동물 찾기

> [프로그래머스_이름에 EL이 들어가는 동물 찾기](https://programmers.co.kr/learn/courses/30/lessons/59047)

```mysql
-- 코드를 입력하세요
SELECT ANIMAL_ID, NAME
FROM ANIMAL_INS
WHERE UPPER(NAME) LIKE UPPER('%EL%') AND ANIMAL_TYPE = 'Dog'
ORDER BY NAME;
```



## 프로그래머스_중성화여부파악하기

> [프로그래머스_중성화여부파악하기](https://programmers.co.kr/learn/courses/30/lessons/59049)

```mysql
-- 코드를 입력하세요
SELECT ANIMAL_ID,
NAME,
CASE WHEN SEX_UPON_INTAKE LIKE '%Neutered%' OR SEX_UPON_INTAKE LIKE '%Spayed%'
THEN 'O'
ELSE 'X' END AS '중성화'
FROM ANIMAL_INS
ORDER BY ANIMAL_ID;
```

- 다른코드

```mysql
-- 코드를 입력하세요
SELECT ANIMAL_ID,
       NAME,
       CASE WHEN SEX_UPON_INTAKE LIKE '%Neutered%' OR SEX_UPON_INTAKE LIKE '%Spayed%'
            THEN 'O'
            ELSE 'X' END AS '중성화'
FROM ANIMAL_INS

-- 코드를 입력하세요
select animal_id, name, if(sex_upon_intake like 'Intact%', 'X', 'O') 
from animal_ins
order by animal_id;
```



## 프로그래머스_오랜기간보호한동물(2)

> [프로그래머스_오랜기간보호한동물(2)](https://programmers.co.kr/learn/courses/30/lessons/59411)

```mysql
-- 코드를 입력하세요
SELECT O.ANIMAL_ID,
O.NAME
FROM ANIMAL_OUTS AS O
JOIN ANIMAL_INS AS I
USING(ANIMAL_ID)
ORDER BY O.DATETIME - I.DATETIME DESC
LIMIT 2;
```

- 다른 코드

```MYSQL
SELECT ANIMAL_ID, O.NAME
FROM ANIMAL_OUTS O LEFT JOIN ANIMAL_INS I USING(ANIMAL_ID)
ORDER BY (O.DATETIME - I.DATETIME) DESC
LIMIT 2;

SELECT ANIMAL_ID,
       ANIMAL_INS.NAME
FROM ANIMAL_INS
    INNER JOIN ANIMAL_OUTS
        USING (ANIMAL_ID)
ORDER BY DATEDIFF(ANIMAL_OUTS.DATETIME,ANIMAL_INS.DATETIME) DESC
LIMIT 2;
```



## 프로그래머스_DATETIME에서 DATE로 형변환

> [프로그래머스_DATETIME에서 DATE로 형변환](https://programmers.co.kr/learn/courses/30/lessons/59414)

```mysql
-- 코드를 입력하세요
SELECT ANIMAL_ID,
NAME,
DATE_FORMAT(DATETIME,'%Y-%m-%d') AS '날짜'
FROM ANIMAL_INS 
ORDER BY ANIMAL_ID;
```



## 프로그래머스_헤비유저가소유한장소

> [프로그래머스_헤비유저가소유한장소](https://programmers.co.kr/learn/courses/30/lessons/77487)
>
> 이 서비스에서는 공간을 둘 이상 등록한 사람을 "헤비 유저"라고 부릅니다. 헤비 유저가 등록한 공간의 정보를 아이디 순으로 조회

```mysql
SELECT *
FROM PLACES
WHERE HOST_ID IN (
SELECT HOST_ID FROM PLACES
GROUP BY HOST_ID
HAVING COUNT(ID) >= 2)
ORDER BY ID;
```



## 프로그래머스_우유와요거트가 담긴 장바구니

> [프로그래머스_우유와요거트가 담긴 장바구니](https://programmers.co.kr/learn/courses/30/lessons/62284)

```mysql
-- 코드를 입력하세요
SELECT C.CART_ID
FROM CART_PRODUCTS C
WHERE C.NAME LIKE "%Milk%" AND C.CART_ID IN (
SELECT CART_ID
FROM CART_PRODUCTS
WHERE NAME LIKE "%Yogurt%")
GROUP BY CART_ID
ORDER BY CART_ID;
```

```mysql
-- 코드를 입력하세요
SELECT Y.CART_ID
FROM CART_PRODUCTS AS M
JOIN (
SELECT NAME, CART_ID
FROM CART_PRODUCTS
WHERE NAME LIKE "%Yogurt%") AS Y
USING(CART_ID)
WHERE M.NAME LIKE "%Milk%"
GROUP BY CART_ID
ORDER BY CART_ID;
```

- 다른코드

```mysql
SELECT a.cart_id
from cart_products as a, cart_products as b
where a.cart_id=b.cart_id and a.name='milk' and b.name='yogurt'
order by a.cart_id;
```

```mysql
SELECT
    CART_ID
FROM
    CART_PRODUCTS
GROUP BY
    CART_ID
HAVING
    GROUP_CONCAT(NAME SEPARATOR ' ') LIKE '%Milk%'
    AND
    GROUP_CONCAT(NAME SEPARATOR ' ') LIKE '%Yogurt%'
```

```mysql
select c.cart_id
from cart_products c
where c.cart_id in (select cart_id from cart_products  where name = 'Yogurt')
and c.name = 'Milk'
group by cart_id
order by id
```

```mysql
with temp as ( 
    select distinct cart_id, name
from cart_products
where name = 'Milk' OR name = 'Yogurt'
)

SELECT temp.cart_id
FROM TEMP
group by cart_id
having COUNT(*) = 2
```



```mysql
select b.CART_ID 
from (
select a.CART_ID , count(*) CNT 
    from (
            select *
            from CART_PRODUCTS
            where NAME = 'Milk' or NAME = 'Yogurt' ) a
            group by a.CART_ID
            having CNT >= 2
            order by a.CART_ID
    ) b
```


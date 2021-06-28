# SUM, MAX, MIN

[toc]

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
SELECT COUNT(DISTINCT NAME) FROM ANIMAL_INS;
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
SELECT DISTINCT(NAME), COUNT(NAME) AS COUNT 
FROM ANIMAL_INS 
-- WHERE NAME IS NOT NULL 
GROUP BY NAME 
HAVING COUNT(NAME) >= 2 
ORDER BY NAME;
```



## 프로그래머스_입양시각구하기(1)

> [프로그래머스_입양시각구하기(1)](https://programmers.co.kr/learn/courses/30/lessons/59412)

```mysql
-- 코드를 입력하세요
SELECT HOUR(DATETIME), COUNT(ANIMAL_ID) 
FROM ANIMAL_OUTS
WHERE DATE_FORMAT(DATETIME,'%H:%i') BETWEEN '09:00' AND '19:59'
GROUP BY HOUR(DATETIME)
ORDER BY HOUR(DATETIME);
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

```mysql
-- 코드를 입력하세요
WITH RECURSIVE TIME AS (
SELECT 0 AS H
UNION ALL
SELECT H+1 FROM TIAME WHERE H < 23)

SELECT H AS HOUR, COUNT(DATETIME) AS COUNT
FROM TIME
LEFT JOIN ANIMAL_OUTS ON H = HOUR(DATETIME)
GROUP BY H
ORDER BY H;
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


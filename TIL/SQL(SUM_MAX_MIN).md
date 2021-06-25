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
SELECT ANIMAL_TYPE, COUNT(ANIMAL_ID) AS count FROM ANIMAL_INS WHERE ANIMAL_TYPE IN ("Cat","Dog") GROUP BY ANIMAL_TYPE ORDER BY ANIMAL_TYPE;
```


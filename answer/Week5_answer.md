## 문제 1

> **🧚Q. 광윤이는 사용자 로그 데이터에서, 2021년에 접속한 사용자 수를  집계하려고 했습니다. 그는 여러 SQL 쿼리들을 실행해봤지만, 그 중 일부는 문법적으로 잘못되어 실행되지 않았습니다. 다음 보기 중 틀린 쿼리를 모두 골라보세요 (복수 선택 가능)**

~~~sql
1. SELECT COUNT(*)  
   FROM user_log  
   WHERE EXTRACT(YEAR FROM login_date) = 2021;

2. SELECT EXTRACT(YEAR FROM login_date), COUNT(*)  
   FROM user_log  
   GROUP BY EXTRACT(YEAR FROM login_date);

3. SELECT COUNT(*)  
   FROM user_log  
   WHERE login_date = '2021';

4. SELECT COUNT(*)  
   FROM user_log  
   WHERE login_date BETWEEN '2021-01-01' AND '2021-12-31';
~~~

<!-- 틀린쿼리에 대한 오류의 원인도 같이 작성해주세요. 문제에서 제공된 login_data 컬럼은 DATE type의 데이터를 가지고 있다고 가정하시면 됩니다. -->

~~~
정답 : 3번
login_date = '2021'은 날짜 전체 형식이 맞지 않다. 대부분의 데이터베이스에서 login_date는 DATE 또는 DATETIME이므로, 연도만 비교하면 오류가 발생하거나 빈 결과가 나올 수 있습니다.

1번 : EXTRACT(YEAR FROM login_date)는 날짜에서 연도만 추출하여 비교하는 정상적인 방법입니다.
2번 : 연도별로 그룹핑하여 건수를 세는 집계 쿼리로 문법적으로 오류가 없습니다.
4번 : 날짜 범위 조건은 BETWEEN '2021-01-01' AND '2021-12-31'처럼 사용하는 것이 적절합니다.
~~~



## 문제 2

> **🧚Q. 혜성이는 포켓몬 타입에 따라 설명을 부여하는 쿼리를 작성했습니다. type 1 컬럼의 값에 따라 조건을 분기했으며, 다음 SQL 쿼리를 실행했습니다.**

~~~sql
SELECT name,
       CASE 
         WHEN type1 = 'Fire' THEN 'Hot'
         WHEN type1 = 'Water' THEN 'Cool'
         ELSE 'Normal'
       END AS type_description
FROM pokemon;
~~~

> **다음 중 type_description의 결과가 'Normal'로 출력될 포켓몬은?**

| **name**   | **type1** |
| ---------- | --------- |
| Pikachu    | Electric  |
| Charmander | Fire      |
| Squirtle   | Water     |
| Bulbasaur  | Grass     |

<!-- 근거와 함께 답을 작성해주세요 -->

~~~
정답 : Pikachu, Bulbasaur
조건 분기를 보면 type1에서 'Fire' -> 'Hot', 'Water' -> 'Cool' 으로 되어 있고 그 외는 모두 'Normal'로 되어있는 것을 확인할 수 있다. 따라서 각각 1,2번째 조건과 일치하는 Charmander, Squirtle는 해당되지 않고, Pikachu와 Bulbasaur은 ELSE로 'Normal'에 속하는 포켓몬들이다. 
~~~

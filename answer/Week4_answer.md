## 문제 1

> **🧚Q. 프로그래머스 문제를 풀던 서현이는 여러 번의 시행착오 끝에 결국 혼자 해결하기 어려워 오류 메시지를 공유하며 도움을 요청했습니다. 여러분들이 오류 메시지를 확인하고, 해당 SQL 쿼리에서 어떤 부분이 잘못되었는지 오류 메시지를 해석하고 찾아 설명해주세요.**

~~~sql
# 조건에 맞는 회원 수 구하기 (SELECT, COUNT) 
# 서현이의 SQL 첫 번째 풀이
SELECT COUNT(AGE, JOINED)
FROM USER_INFO
WHERE AGE BETWEEN 20 AND 29
  AND JOINED BETWEEN '2021-01-01' AND '2021-12-31';
  
오류 메시지 : Error: Number of arguments does not match for aggregate function COUNT
 
# 수정하고 난 이후 두 번째 풀이
SELECT AGE, COUNT(*)
FROM USER_INFO
WHERE AGE BETWEEN 20 AND 29
  AND JOINED BETWEEN '2021-01-01' AND '2021-12-31';
  
오류 메시지 : SELECT list expression references column AGE which is neither grouped nor aggregated
~~~


~~~
정답 : 
1) Number of arguments does not match for aggregate function COUNT
오류 메시지를 해석하면 COUNT 함수는 하나의 인자만 받거나, COUNT(*), COUNT(column)처럼 사용해야 한다. 
첫 번째 풀이를 보면 COUNT(AGE, JOINED) 처럼 두 개의 인자를 사용했는데 이것이 문법 오류를 발생시킨 것으로 보인다. 수정하기 위해서 COUNT(*) 또는 COUNT(AGE)처럼 사용해야 한다. 

2) SELECT list expression references column AGE which is neither grouped nor aggregated
두 번째 오류 메시지를 해석하면 SELECT 절에 있는 AGE는 집계함수도 아니고, GROUP BY 에도 포함되지 않는다. SQL에서는 집계함수를 사용하면서 일반 컬럼을 함께 조회하기 위해서는 그 일반 컬럼은 반드시 GROUP BY 절에 포함되어야 한다. 
따라서 마지막 줄에 GROUP BY AGE 한 줄을 추가함으로써 수정할 수 있다. 
~~~

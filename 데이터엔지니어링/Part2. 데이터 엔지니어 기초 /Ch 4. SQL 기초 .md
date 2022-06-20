## SQL 기초

---

### 1. SQL 개요, SQL 커맨드들

- SQL은 Structured Query Language(구조적 질의 언어)의 줄임말로, 관계형 데이터베이스 시스템(RDBMS)에서 자료를 관리 및 처리하기 위해 설계된 언어

### 2. SELECT(1)

- SELECT

SELECT 문은 데이터를 조회하는 쿼리문에 사용된다. 그런테 쿼리문이 적힌 순서가 아닌 정해진 순서대로 작동하게 된다. 

- SELECT 실행 순서

> FROM
WHERE
GROUP BY
HAVING
SELECT
ORDER BY
>

예)

```sql
SELECT CustomerId, AVG(Total)
FROM invoices
WHERE CustomerId >= 10
GROUP BY CustomerId
HAVING SUM(Total) >= 30
ORDER BY 2
```


> FROM invoices: 먼저 invoices 테이블에 접근
WHERE CustomerId >= 10: 'CustomerId' 필드가 10 이상인 레코드들을 조회
GROUP BY CustomerId: 'CustomerId' 를 기준으로 그룹화
HAVING SUM(Total) >= 30: 'Total' 필드의 값들의 합이 30 이상인 결과들만 필터
SELECT CustomerId, AVG(Total): 조회된 결과에서 'CustomerId' 필드와 'Total' 필드의 평균값 가져옴
ORDER BY 2: AVG(Total) 필드를 기준으로 오름차순 정렬
>

- ORDER BY

- WHERE: 컨디션으로 필터를 하겠다는 의미

### 3. SELECT(2)

- SUM

- AVG


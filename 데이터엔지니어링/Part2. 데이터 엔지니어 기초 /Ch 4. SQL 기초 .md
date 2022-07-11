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

    SQLite는 지정되지 않은 순서로 테이블에 데이터를 저장. 이는 테이블의 행이 삽입된 순서대로 있을 수도 있고, 아닐 수도 있음을 의미

    SELECT문을 사용하여 테이블의 데이터를 쿼리하는 경우에 결과 집합의 행 순서가 지정되지 않는다.
    이 때, 결과 집합을 정렬하기 위해 ORDER BY절을 SELECT문에 추가!

- WHERE: 컨디션으로 필터를 하겠다는 의미

### 3. SELECT(2)


```SQL
-- SUM, AVG

SELECT * FROM Salaries WHERE playerID  = 'rodrial01' ORDER BY yearID ASC ;

SELECT SUM(salary)
FROM Salaries 
WHERE playerID = 'rodrial01';
```

```SQl
-- Concat Function, DISTINCT
	--top Ten Salaries and Player Names

SELECT nameFirst || ' ' || nameLast From People p  Limit 10;
SELECT nameFirst || ' ' || nameLast AS name From People p  Limit 10;

SELECT nameFirst || ' ' || nameLast AS name From People p  WHERE playerID  = 'rodrial01';

SELECT COUNT(*) FROM People p; 

SELECT COUNT(DISTINCT(nameFirst || ' ' || nameLast)) FROM People p ;

SELECT nameFirst || ' ' || nameLast AS name, count(*) FROM People p GROUP BY name HAVING count(*) >1;
-- MySQL Version SELECT CONCAT(nameFirst, nameLast) FROM People p LIMIT 10;
```

```SQL
-- 어떤 팀이 역대로 많은 salary를 썼는지
SELECT 
	yearID,
	teamID,
	SUM(salary) AS total_salary
FROM 
	Salaries s 
GROUP BY yearID, teamID 
ORDER BY SUM(salary) DESC;
```

---

### 4. JOIN(1) 

```SQL
--JOIN

SELECT
	playerID,
	salary
FROM 
	Salaries s 
ORDER BY salary DESC
LIMIT 20;

SELECT 
	p.nameFirst || ' ' || p.nameLast AS name,
	s.salary 
FROM 
	Salaries s
JOIN People p ON p.playerID = s.playerID 
ORDER BY salary DESC
LIMIT 20;
```

```SQL
--JOIN AND GROUP BY
--TOP paid player for each team in 2010
SELECT 
	s.teamID,
	p.nameFirst || ' ' || p.nameLast AS name,
	MAX(salary)
FROM 
	People p
JOIN Salaries s ON s.playerID = p.playerID 
WHERE 
	s.yearID = 2010
GROUP BY 
	s.teamID 
```

### 5. JOIN(2)

```SQL
-- LEFT JOIN 
	--AllstarFull와 People 에서 playID를 기준으로 다 묶어 한쪽 테이블엔 있지만 다른쪽에 없는 경우 NULL값으로 확인되는 것을 볼 수 있음.
	
SELECT 
	*
FROM 
	People p 
LEFT JOIN
	AllstarFull af ON af.playerID =p.playerID 
LIMIT 20;
```

```SQL
-- LEFT JOIN
SELECT
	COUNT(DISTINCT p.playerID)
FROM 
	People p 
LEFT JOIN
	AllstarFull af ON af.playerID = p.playerID

-- 만약 그냥 JOIN을 한다면
SELECT
	COUNT(DISTINCT p.playerID)
FROM 
	People p 
JOIN
	AllstarFull af ON af.playerID = p.playerID
```

```SQL
-- WHERE b.key IS NULL
    -- A에는 있지만 B에는 없는 애들만 가져와줘~
SELECT
	COUNT(DISTINCT p.playerID)
FROM 
	People p 
LEFT JOIN
	AllstarFull af ON af.playerID = p.playerID
WHERE af.playerID IS NULL;
```

```SQL
-- LEFT JOIN AND GROUP BY
    -- 이 경우 1의 값이 1번인지, NULL값인지 구분하기가 어렵다. 그래서 잘 생각하고 사용해야한다.
    
SELECT 
	p.playerID,
	COUNT(*) 
FROM
	People p 
LEFT JOIN
	AllstarFull af ON af.playerID = p.playerID 
GROUP BY 1
LIMIT 20;

-- 그래서 보통 1은 무시하고 ORDERBY랑 같이 사용하여 순위 확인할 때 사용
-- JOIN을 사용해도 되지만 모든선수에 대한 값을 가지고 싶을땐 이런식으로 사용
SELECT 
	p.playerID,
	COUNT(*) 
FROM
	People p 
LEFT JOIN
	AllstarFull af ON af.playerID = p.playerID 
GROUP BY 1
ORDER BY COUNT(*) DESC 
LIMIT 20;
```

```SQL
-- RIGHT JOIN
    -- LEFT JOIN과 같은데 보통은 LEFT를 사용하여 왼쪽을 기준으로 하는 경우가 많음
SELECT
	COUNT(DISTINCT p.playerID)
FROM 
    AllstarFull af	
RIGHT JOIN
	People p ON af.playerID = p.playerID
```

---

## SQL 기초

---

### 1. SQL 개요, SQL 커맨드들

---

- SQL은 Structured Query Language(구조적 질의 언어)의 줄임말로, 관계형 데이터베이스 시스템(RDBMS)에서 자료를 관리 및 처리하기 위해 설계된 언어

### SELECT

---

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
```
<img width="796" alt="스크린샷 2022-07-11 오후 1 07 25" src="https://user-images.githubusercontent.com/86764734/178269561-7f59f5cb-05df-49d6-b476-e3cb97e65e24.png">

<img width="772" alt="스크린샷 2022-07-11 오후 1 34 17" src="https://user-images.githubusercontent.com/86764734/178269579-5c12ef65-3a30-4244-a272-d8b08b82b97a.png">

```sql
SELECT nameFirst || ' ' || nameLast AS name From People p  WHERE playerID  = 'rodrial01';

SELECT COUNT(*) FROM People p; 

SELECT COUNT(DISTINCT(nameFirst || ' ' || nameLast)) FROM People p ;

SELECT nameFirst || ' ' || nameLast AS name, count(*) FROM People p GROUP BY name HAVING count(*) >1;
-- MySQL Version SELECT CONCAT(nameFirst, nameLast) FROM People p LIMIT 10;
```
<img width="985" alt="스크린샷 2022-07-11 오후 1 36 17" src="https://user-images.githubusercontent.com/86764734/178269596-51a3f89a-5f04-459a-b795-00ea171fa3f9.png">



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

<img width="654" alt="스크린샷 2022-07-11 오후 2 28 40" src="https://user-images.githubusercontent.com/86764734/178269612-e654ca1b-561a-4eec-a562-d9f15b45af2d.png">
---

### JOIN

--- 

<img width="843" alt="JOIN들" src="https://user-images.githubusercontent.com/86764734/178269631-24f4995a-4570-40ce-aed7-4d0060abe5ce.png">


```SQL
--JOIN

SELECT
	playerID,
	salary
FROM 
	Salaries s 
ORDER BY salary DESC
LIMIT 20;
```

<img width="662" alt="스크린샷 2022-07-11 오후 3 00 52" src="https://user-images.githubusercontent.com/86764734/178270781-824d2e64-7557-4c6a-9642-20ad8dbeade9.png">

```sql
SELECT 
	p.nameFirst || ' ' || p.nameLast AS name,
	s.salary 
FROM 
	Salaries s
JOIN People p ON p.playerID = s.playerID 
ORDER BY salary DESC
LIMIT 20;
```

<img width="1164" alt="스크린샷 2022-07-11 오후 3 33 21" src="https://user-images.githubusercontent.com/86764734/178269664-14dece1d-fefb-4d87-8e6b-85fb03376052.png">

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

<img width="764" alt="스크린샷 2022-07-11 오후 3 58 47" src="https://user-images.githubusercontent.com/86764734/178271347-b5f2a706-9d76-4433-9db1-e241bc84a0f5.png">


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

<img width="1371" alt="스크린샷 2022-07-11 오후 4 50 30" src="https://user-images.githubusercontent.com/86764734/178271534-1c53af1c-95ac-4479-976e-723dd58592e5.png">

```SQL
-- LEFT JOIN
SELECT
	COUNT(DISTINCT p.playerID)
FROM 
	People p 
LEFT JOIN
	AllstarFull af ON af.playerID = p.playerID
```
<img width="895" alt="스크린샷 2022-07-11 오후 4 53 19" src="https://user-images.githubusercontent.com/86764734/178271733-df1c8229-1ddf-4dda-8968-f3cfab1fe48b.png">

```sql
-- 만약 그냥 JOIN을 한다면
SELECT
	COUNT(DISTINCT p.playerID)
FROM 
	People p 
JOIN
	AllstarFull af ON af.playerID = p.playerID
```


<img width="774" alt="스크린샷 2022-07-11 오후 4 55 52" src="https://user-images.githubusercontent.com/86764734/178272029-7b0bd0b8-ac56-41c0-ab6f-236d3f34bee4.png">

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
<img width="709" alt="스크린샷 2022-07-11 오후 4 58 33" src="https://user-images.githubusercontent.com/86764734/178272192-1e162d4d-10b0-4781-9f50-286cc2fde3f2.png">

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

```

<img width="708" alt="스크린샷 2022-07-11 오후 5 09 17" src="https://user-images.githubusercontent.com/86764734/178272485-ce55ae86-ac2a-4f0b-a25b-b1e502fb72f3.png">

```sql
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
<img width="678" alt="스크린샷 2022-07-11 오후 5 12 31" src="https://user-images.githubusercontent.com/86764734/178272537-85ee6cb1-6ffe-4418-b3ad-8c41e754aec8.png">

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


### 데이터 타입들 및 키 값들 & 데이터베이스 테이블 생성

---

- Primary Key
- Foreign Key
- Unique
    - 중복되는 값이 들어오지 못하게

```sql
-- Table 생성
CREATE TABLE mytable (id INT, name VARCHAR(255), debut DATE);

-- PRIMARY KEY 설정
CREATE TABLE mytable2 (id INTEGER PRIMARY KEY AUTOINCREMENT, name VARCHAR(255), dabut DATE);

CREATE TABLE "mytable2" ([id] INTEGER PRIMARY KEY AUTOINCREMENT, [name] VARCHAR(255), [dabut] DATE);

-- tamble에 데이터 저장
INSERT INTO mytable2 (name, dabut) VALUES ('ssu', '2022-07-11');

SELECT * FROM mytable2;

```
- Table 생성
<img width="814" alt="스크린샷 2022-07-11 오후 8 27 43" src="https://user-images.githubusercontent.com/86764734/178269790-95fbc2b3-49b2-4fa3-8756-19ff25626cd7.png">

- PRIMARY KEY 설정
<img width="794" alt="스크린샷 2022-07-11 오후 8 32 32" src="https://user-images.githubusercontent.com/86764734/178269806-7fe0fd62-098b-4a52-af33-bfbaebb51326.png">

- tamble에 데이터 저장
<img width="1047" alt="스크린샷 2022-07-11 오후 8 39 22" src="https://user-images.githubusercontent.com/86764734/178269824-e3771342-988c-44a4-a81c-140be3511814.png">
---

### UPDATE, REPLACE, INSERT

---

```sql
-- INSERT
    -- AUTOINCREMENT이기 때문에 id는 따로 지정하지 않아도 된다.

INSERT INTO mytable2 (name, dabut) VALUES ('hi', '2022-07-12');

-- 만약 id값을 임의로 지정해준다면, 다음 값은 AUTOINCREMENT의 영향으로 자동으로 다음 번호 지정
INSERT INTO mytable2 (id, name, dabut) VALUES ('365', 'hi', '2022-07-12');

INSERT INTO mytable2 (name, dabut) VALUES ('hello', '2022-07-13');

SELECT * FROM mytable2;
```

<img width="783" alt="스크린샷 2022-07-11 오후 9 35 57" src="https://user-images.githubusercontent.com/86764734/178273168-1af0c639-6dd4-4f6a-a013-d677cd4333a0.png">

```sql
-- UPDATE 
    -- id가 2인 데이터의 'name'을 'haha'로 update
    -- 만약 키값이 테이블에 없다면 update되지 않는다
UPDATE mytable2 
SET name = 'haha'
WHERE id = 2;

SELECT * FROM mytable2;
```
<img width="612" alt="스크린샷 2022-07-11 오후 9 40 39" src="https://user-images.githubusercontent.com/86764734/178273493-0541c826-428b-49dd-8e8f-b7e9d5360fa7.png">

```sql
-- REPLACE
    -- id가 '365'인 데이터의 'name', 'dabut'값을 'hoho', '2022-07-13'로 바꿔줘

REPLACE INTO mytable2 (id, name, dabut) VALUES ('365', 'hoho', '2022-07-13');

-- 만약 해당 key값이 없으면 하나의 row를 새로 생성
REPLACE INTO mytable2 (id, name, dabut) VALUES ('7', 'hello', '2022-07-14');
```

<img width="807" alt="스크린샷 2022-07-11 오후 9 45 48" src="https://user-images.githubusercontent.com/86764734/178273619-326d2a2b-ef16-47c0-8949-c04656e7a654.png">

<img width="837" alt="스크린샷 2022-07-11 오후 9 50 03" src="https://user-images.githubusercontent.com/86764734/178274034-6013b103-81a2-4e05-88be-b24e8d9e8e86.png">

```sql
-- INSERT OR IGNORE
    -- 우리가 id를 키로 설정했기 때문에 이미 존재하는 key값일 경우 IGNORE
INSERT OR IGNORE INTO mytable2 (id, name, dabut) VALUES ('7', 'ssu', '2022-07-14');

-- 만약 그냥 INSERT 진행한다면 key값이 중복이 되기 때문에 에러
    -- 이미 있는 데이터를 보존하고 지속적으로 데이터를 보낼때 오류가 생기지 않게 하기 위해 자주사용
INSERT INTO mytable2 (id, name, dabut) VALUES ('7', 'ssu', '2022-07-14');
```

<img width="880" alt="스크린샷 2022-07-11 오후 9 52 37" src="https://user-images.githubusercontent.com/86764734/178274238-0a3b6fc3-ef86-455d-9fd5-be82c3518c6f.png">

<img width="882" alt="스크린샷 2022-07-11 오후 9 55 32" src="https://user-images.githubusercontent.com/86764734/178274363-6dd33760-9355-4bf3-870a-951d06e7b367.png">

### DELETE, ALTER, DROP

---

```sql
-- DELETE
	-- mytable2에서 id가 1인 row 삭제
DELETE FROM mytable2 WHERE id = 1;

-- 만약 WHERE을 통해 지정해주지 않으면 테이블전체가 삭제되니까 조심!!
DELETE FROM mytable2;
```

```sql
-- ALTER
		-- TABLE 이름 변경

ALTER TABLE mytable2 RENAME TO players;

SELECT * FROM mytable2;
```

```sql
-- COLUMN 추가

ALTER TABLE players ADD COLUMN DAB date;

SELECT * FROM players;
```

```sql
-- DROP
DROP TABLE mytable;
SELECT * FROM mytable;
```
---

### Functions

---

```sql

-- character
SELECT * FROM players;

-- SUBSTRING 1번 부터 2번까지 가져온다
SELECT SUBSTR(name, 1, 2) FROM players; 

-- case sensitive
SELECT UPPER(name) FROM players;
 
-- LENGTH
SELECT LENGTH(name) FROM players;

-- MAX, AVG, COUNT, SUM
SELECT MAX(LENGTH(name)) FROM players;
```

```sql
-- DATE
SELECT DATE('NOW');

SELECT CURRENT_TIMESTAMP;
SELECT DATE(CURRENT_TIMESTAMP);

-- 1일을 추가해
SELECT DATETIME(CURRENT_TIMESTAMP, '+1 DAY')

-- CASE WHEN
SELECT id, name,
 CASE WHEN
	name = 'hello' THEN 'OK'
 WHEN name = 'haha' THEN 'OK2'
 ELSE 'NOT OK'
 END AS 'name ok', dabut
FROM players;
```



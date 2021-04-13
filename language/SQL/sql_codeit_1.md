# SQL로 하는 데이터분석

## 01. 데이터베이스와 테이블
* 데이터베이스
    * 데이터베이스란 일정한 체계 속에 저장된 데이터의 집합
    * 테이블 단위로 저장
    * 하나의 데이터베이스 안에는 여러 개의 테이블로 저장

* 테이블의 row와 column
    * row(행): 객체
    * column(열): 객체의 속성

* DBMS와 SQL
    * DataBaseManagementSystem: 사용자와 데이터베이스 사이의 매개
        * Mysql, Oracle, MariaDB, SQLServer, SQLite 등
    * Structured Query Language: DBMS에 명령을 내리기 위해 사용하는 언어
        * 표준SQL을 사용하되 DBMS마다 조금씩 다르다.

* DBMS 구조
    * client를 통해 server에 접속하는 구조로 되어 있습니다.
    * 실행되고 있는 server에 client를 이용해서 접속한 후, 원하는 명령을 내린다.

* SQL 사용법
    * 데이터베이스 생성하기
        * CREATE DATABASE {데이터베이스 이름}
        * 데이터베이스=SCHEMAS
    * sys 데이터베이스의 의미: MySQL 서버의 성능 등 관련 정보들을 갖고 있는 데이터베이스, 성능저하 없이 효율적으로 작업하는지 체크

## 02. 테이블 생성
* 테이블 생성
    * SQL문
    * CSV(Comma Separated Values) 파일 임포트

* primary key(기본키): 테이블에서 하나의 row를 고유하게 식별할 수 있도록 해주는 column, 중복 불가능
    * Natural Key: 실제로 어떤 개체가 갖고 있는 속성을 나타내는 컬럼이 Primary Key가 됐을 때
    * Surrogate Key: 속성을 직접적으로 나타내는 것이 아니라 인위적으로 생성한 칼럼

* Not NULL의 의미
    * NULL 값이 존재하지 않는 상태
    * 이 컬럼에는 반드시 어떤 값이 존재해야한다.
    * PK는 NN이어야 한다.

* AI: Auto Increment, 자동증가
    * PK -> Suggorate Key에서 사용

* DATE: 날짜 값 타입

## 03. 데이터 조회
```sql
SELECT * FROM database.member;
```
특정 조건을 만족하는 sql문
```sql
SELECT * FROM database.member WHERE email='a@naver.com';
```

* SQL문 작성 형식
    * SQL문 끝에는 항상 ;을 써줘야 한다.
    * SQL문 안에는 공백이나 개행 등을 자유롭게 넣을 수 있다.
    * SQL문의 대소문자 구분 문자: 예약어 대문자 사용 권장
    * 데이터베이스 이름과 테이블 이름 database.table; 권장

* 조건을 나타내는 방법
나이
```sql
SELECT * FROM database.member
WHERE age
BETWEEN 30 AND 39;
```
```sql
SELECT * FROM database.member
WHERE age
NOT BETWEEN 30 AND 39;
```
날짜
```sql
SELECT * FROM database.member
WHERE sign_up_day > '2019-01-01';
```
```sql
SELECT * FROM database.member
WHERE sign_up_day 
BETWEEN '2018-01-01' AND '2018-12-31';
```

* 문자열 패턴 매칭 조건

서울로 시작하는 모든 문자열 조회
```sql
SELECT * FROM database.member
WHERE adress
LIKE '서울%';
```

고양시가 포함된 모든 문자열 조회
```sql
SELECT * FROM database.member
WHERE adress
LIKE '%고양시%';
```

그 밖의 조건 표현식

* !=,<>: 같지 않음
* IN(a,b): a,b 중에 있는
* _ : 한글자

함수

* 1.연도, 월, 일 추출
YEAR MONTH DAYOFMONTH

2. 날짜 간의 차이
DATADIFF(a,b) : 차이 일수를 알려준다.
DATADIFF(a,CURDATE()): 오늘 날짜와의 차이
DATEDIFF(sign_up_dat,birthday)/365: 몇살 때 가입

3. 날짜 더하기 빼기
DATE_ADD(sign_up_day, INTERVAL 300 DAY): 300일 후의 날짜
DATE_SUB(sign_up_day, INTERVAL 250 DAY): 250일 전의 날짜

4. UNIX Timestamp: 숫자로 날짜시간 표현
UNIX_TIMESTAMP(sign_up_day): 가입 후 몇 초가 지난 것인지
FROM_UNIXTIME(UNIX_TIMESTAMP(sign_up_day)): 원래의 날짜로 변환

날짜, 시간 관련 데이터 타입 : https://dev.mysql.com/doc/refman/8.0/en/date-and-time-types.html

날짜, 시간 관련 함수 : https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html

* 여러 개의 조건 걸기
AND, OR
```sql
SELECT * FROM database.member
WHERE gender = 'm'
    AND adresss LIKE '서울%'
    AND age BETWEEN 25 and 29;
```
```sql
SELECT * FROM database.member
WHERE MONTH(sign_up_day) BETWEEN 3 AND 5
    OR MONTH(sign_up_day) BETWEEN 9 AND 11;
```
```sql
SELECT * FROM database.member
WHERE (gender = 'm' AND height >= 180)
    OR (gender = 'f' AND height >= 170);
```
먼저 실행해야 하는 부분 괄호쳐야함
AND가 OR보다 우선순위 높음

* 문자열 매칭 패턴 조건을 사용할 때 주의할 점

LIKE : 문자열 패턴 매칭 조건을 걸기 위해 사용되는 키워드 
% : 임의의 길의를 가진 문자열(0자도 포함) 
_ : 한 자리의 문자

1. 이스케이핑(escaping)문제
%을 조회할때 '%\%%'
'을 조회할 때 '%\'%'
_을 조회할 때 '%\_%'

2. 대소문자 구분 문제
'%g%' : g,G 모두 조회
기본설정->ci->대소문자를 구별하지 않겠다는 뜻
BINARY '%g%': g만 조회
BINARY '%G%': G만 조회
BINARY: 0,1이 정확하게 일치하는 값 찾음

### 데이터 정렬해서 보기
```sql
SELECT * FROM database.member
ORDER BY hieght ASC;
```
ASC: 오름차순 정렬. 기본 정렬

```sql
SELECT * FROM database.member
ORDER BY hieght DESC;
```
ASC: 내림차순 정렬.

```sql
SELECT * FROM database.member
WHERE gender = 'm'
    AND weight >= 70
ORDER BY hieght ASC;
```

```sql
SELECT sign_up_day, email FROM database.member
ORDER BY YEAR(sign_up_day) DESC, email ASC;
```
가입연도 기준 내림차순, 같다면 이메일 기준 오름차순
정렬 기준 여러 개, 이름 먼저 쓴 게 우선


### 작성순서 지켜야 실행이 잘됨
FROM -> WHERE -> ORDER BY -> LIMIT
https://dev.mysql.com/doc/refman/8.0/en/select.html

### 정렬할 때 주의할 점
INT와 TEXT 정렬 방식 다름
일시적 CAST함수 쓰기
CAST(data As signed)


### 데이터 일부만 추려보기
```sql
SELECT * FROM database.member
ORDER BY sign_up_day DESC
LIMIT 10;
```
LIMIT 한도, 10개 추리기

```sql
SELECT * FROM database.member
ORDER BY sign_up_day DESC
LIMIT 8,2;
```
8번째 로우부터 총 2개의 로우 추려라
0부터 시작

## LIMIT와 Pagination
페이지를 누를 때마다 SQL문 실행
```sql
SELECT * FROM db.search_result ~ ORDER BY registration_date DESC LIMIT 0, 10
SELECT * FROM db.search_result ~ ORDER BY registration_date DESC LIMIT 10, 10
```
위와 같은 예시

## 데이터 분석

### 데이터의 특성 구하기
집계함수
```sql
SELECT COUNT(email) FROM database.member //row수
SELECT COUNT(height) FROM database.member 
SELECT COUNT(*) FROM database.member 
SELECT MAX(height) FROM database.member 
SELECT MIN(height) FROM database.member 
SELECT AVG(height) FROM database.member 
```
COUNT는 row 수를 알려준다. Null의 개수는 제외한다.
COUNT(*) 전체 row수를 알려준다.
가장 큰 값은 MAX, 가장 작은 값 MIN, 평균값은 AVG이다. AVG는 null 제외하고 계산.

산술함수
SUM : 합계
STD: 표준편차
ABS: 절대값
SQRT: 제곱근
CEIL: 올림
FLOOR: 내림
ROUND: 반올림

(1) 집계 함수는 특정 컬럼의 여러 row의 값들을 동시에 고려해서 실행되는 함수이고
(2) 산술 함수는 특정 컬럼의 각 row의 값마다 실행되는 함수

### null을 다루는 방법
null: 값이 없음.
null이 있는 데이터를 분석

```sql
SELECT * FROM databases.member WHERE adress IS NULL;
SELECT * FROM databases.member WHERE adress IS NOT NULL;
```
```sql
SELECT * FROM database.member 
    WHERE adress IS NULL
        OR weight IS NULL
        OR address IS NULL;
```
```sql
SELECT 
    COALESCE(height,'####'), //null인 경우 #### 출력
    COALESCE(weight,'---'),
    COALESCE(address,'@@@'),
FROM databases.table;
```

IS NULL과 = NULL은 다르다.
NULL은 어떤 연산을 해도 NULL이다.

### 이상한 값을 제외하고 싶다면
```sql
SELECT AVG(age) FROM databases.table
    WHERE age BETWEEN 5 AND 100;
```
```sql
SELECT AVG(age) FROM databases.table
    WHERE adress NOT LIKE'%호';
```

### 컬럼끼리 계산하기
```sql
SELECT weight/((height/100)*(height/100))
FROM databases.table;
```
컬럼끼리 +-*/% 모두 가능
식 안에 하나라도 null이 있으면 답은 null

### alias 붙이기
```sql
SELECT 
    height AS 키,
    weight AS 몸무게,
    weight/((height/100)*(height/100)) AS BMI,
    CONCAT(height, 'cm', ',' weight, 'kg' ) AS '키와 몸무게',
FROM databases.table;
```
AS = Alias(별명,별칭)
AS 없이 ' '(스페이스)로도 별칭을 붙일 수 있다.

### 컬럼 값 변환해서 보기
```sql
SELECT 
    weight/((height/100)*(height/100)) AS BMI,
    CONCAT(height, 'cm', ',' weight, 'kg' ) AS '키와 몸무게',

{CASE
    WHEN weight IS NULL OR height is NULL THEN '비만 여부 알 수 없음'
    WHEN weight/((height/100)*(height/100))>=25 THEN '과체중 또는 비만'
    WHEN weight/((height/100)*(height/100))>= 18.5
        AND weight/((height/100)*(height/100)) <25
        THEN 정상
    ELSE '저체충'
END} AS obesity_check

FROM databases.table;
ORDER BY obesity_check ASC;
```

### CASE 함수의 종류
1. 단순 CASE 함수
CASE 컬럼 이름 
  WHEN 값 THEN 값 
  WHEN 값 THEN 값
  WHEN 값 THEN 값
  ELSE 값
END
CASE 문 바로 뒤에 컬럼 이름을 쓰고, 그 컬럼의 값과 어떤 값이 같은지(=)를 비교하는 CASE 함수를 단순 CASE 함수라고 합니다.

2. 검색 CASE 함수
CASE 
  WHEN 조건1 THEN 값
  WHEN 조건2 THEN 값 
  WHEN 조건3 THEN 값 
  ELSE 값
END 
다양한 형태의 조건을 걸 수 있다는 장점

### NULL 다른값으로 변환
1. COALESCE 함수 
COALESCE(height,weight*2.3,'N/A')
 키가 보통 몸무게에 2.3 을 곱한 값이라고 가정
 height 컬럼도 NULL이고, weight 컬럼도 NULL인 row라면 ‘N/A’가 출력

2. IFNULL 함수
IFNULL(height,'N/A')

3. IF함수
IF(height IS NOT NULL, height, 'NA/A')

4. CASE 함수
CASE 
  WHEN height IS NOT NULL THEN height
  ELSE 'N/A'
END 


### alias를 붙이고 바로 쓸 수 없는 이유
1. 띄어쓰기(스페이스)가 포함된 alias에는 따옴표를 붙여줘야 합니다.
2. SELECT 절에서 설정한 alias를 바로 사용할 수 없는 문제 -> 나중에 서브쿼리로 해결

```sql
SELECT 
    name,
    price,
    price/cost, 
(CASE  
    WHEN price/cost >= 1.7 THEN 'A. 고효율 메뉴'
    WHEN price/cost < 1.7
        AND price/cost >= 1.5 
        THEN 'B. 중효율 메뉴'
    WHEN price/cost < 1.5
        AND price/cost >= 1 
        THEN 'C. 저효율 메뉴'
END) AS efficiency


FROM pizza_price_cost
ORDER BY efficiency DESC, price ASC
LIMIT 6;
```

### 17. 고유값만 보기
중복값 제거!
```sql
SELECT DISTINCT(gender) FROM databases.table;
```
주요 지역 고유값. 가장 앞자리 2자리
```sql
SELECT DISTINCT(SUBSTRING(address, 1, 2)) FROM databases.table;
```
첫 문자부터 앞 2문자

### 18. 고유값의 개수 구하기
```sql
SELECT COUNT(DISTINCT(gender)) FROM databases.table;
```

### 19. 문자열 관련 함수들
1. LENGTH 함수
2. UPPER, LOWER 함수
3. LPAD, RPAD 함수
이 두 함수는 문자열의 왼쪽 또는 오른쪽을 특정 문자열로 채워주는 함수입니다
예를 들어 LPAD(age, 10, ’0’)는 age 컬럼의 값을, 왼쪽에 문자 0을 붙여서 총 10자리로 만드는 함수입니다. 
4. TRIM, LTRIM, RTRIM 함수
(1) LTRIM : 왼쪽 공백 삭제
(2) RTRIM : 오른쪽 공백 삭제
(3) TRIM : 왼쪽, 오른쪽 양쪽 다 공백 삭제

### 20. 그루핑해서 보기
```sql
SELECT gender,COUNT(*) FROM databases.table
GROUP BY gender;
```
m에는 m인 모든 row 포함
f는 f인 모든 row 포함

그룹핑 상태에서는 
COUNT(*), AVG(height)
COUNT(*), AVG(height)
로 실행

그룹바이 후 함수는 그룹끼리 각각 실행된다.

집계함수: 그루핑을 통해 생성된 각 그룹의 수치적인 특성을 구하는 함수
ex) count,avg,min

### 22. 여러 개의 column 그루핑
```sql
SELECT 
    SUBSTRING(address,1,2) as region,
    gender,
    COUNT(*)
FROM databases.table
GROUP BY 
    SUBSTRING(address,1,2),
    gender;
```
세부적으로 그룹 나뉨
주요지역과 성별을 기준으로 분류 (서울,여자/서울,남자)

### 23. 특정 그루핑
```sql
SELECT 
    SUBSTRING(address,1,2) as region,
    gender,
    COUNT(*)
FROM databases.table
GROUP BY 
    SUBSTRING(address,1,2),
    gender
HAVING 
    region IS NOT NULL
    AND gender = 'm';
ORDER BY
    region ASC,
    gender DESC;
```
HAVING : ~을 가지고 있는
보고 싶은 그룹만 선별

WHERE? 의미는 비슷해보이지만 다르다.
WHERE은 
HAVING은 그룹 중에서 다시 필터링


## 규칙
그건 바로 GROUP BY를 사용할 때는, SELECT 절에는 

(1) GROUP BY 뒤에서 사용한 컬럼들 또는

(2) COUNT, MAX 등과 같은 집계 함수만 

쓸 수 있다는 규칙입니다. 이건 거꾸로 말해 GROUP BY 뒤에 쓰지 않은 컬럼 이름을 SELECT 뒤에 쓸 수는 없다는 말입니다.

그런데 GROUP BY 뒤에 쓰지 않은, 그러니까 그루핑 기준으로 사용하지 않은 컬럼명을 

SELECT 절 뒤에 써서 조회하려고 하면, 

각 그룹의 row들 중에서 해당 컬럼의 값을 

어느 row에서 가져와야할지 결정할 수가 없습니다.

## SELECT문 실행 순서
각 절들을, 더 앞에 나와야 하는 순서대로 써보겠습니다. 

SELECT 
FROM
WHERE
GROUP BY
HAVING 
ORDER BY
LIMIT 

각 절의 용도가 뭔지는 다 기억하셔야 합니다. 그런데 이런 작성 순서만큼이나 중요한 사실이 하나 있습니다.

이 사실은 여러분의 SQL 해석 능력을 한층 업그레이드해줄 사실인데요.

그것은 바로 각 절들이 위에 쓴 순서대로 실행되는 것이 아니라

사실은 아래의 순서대로 해석 및 실행된다는 사실입니다. 

FROM
WHERE 
GROUP BY
HAVING 
SELECT
ORDER BY
LIMIT 
어떤 식으로 해석 및 실행되는지를 하나씩 차례대로 살펴보면 다음과 같습니다.

FROM : 어느 테이블을 대상으로 할 것인지를 먼저 결정합니다. 
WHERE : 해당 테이블에서 특정 조건(들)을 만족하는 row들만 선별합니다. 
GROUP BY : row들을 그루핑 기준대로 그루핑합니다. 하나의 그룹은 하나의 row로 표현됩니다.
HAVING : 그루핑 작업 후 생성된 여러 그룹들 중에서, 특정 조건(들)을 만족하는 그룹들만 선별합니다. 
SELECT : 모든 컬럼 또는 특정 컬럼들을 조회합니다. SELECT 절에서 컬럼 이름에 alias를 붙인 게 있다면, 이 이후 단계(ORDER BY, LIMIT)부터는 해당 alias를 사용할 수 있습니다.
ORDER BY : 각 row를 특정 기준에 따라서 정렬합니다. 
LIMIT : 이전 단계까지 조회된 row들 중 일부 row들만을 추립니다.
```sql
SELECT 
    category, 
    main_month, 
    COUNT(*) AS '영화 수', 
    SUM(view_count) AS '총 관객 수'
FROM 2020_movie_report
GROUP BY category, main_month
HAVING 
    main_month = 5
    AND SUM(view_count) >= 3000000
```

### 심화
```sql
SELECT 
    category, 
    main_month, 
    COUNT(*) AS '영화 수', 
    SUM(view_count) AS '총 관객 수'
FROM 2020_movie_report
GROUP BY category, main_month
WITH ROLLUP
HAVING 
    main_month = 5
    AND SUM(view_count) >= 3000000
```
WITH ROLLUP
region만을 기준으로 한 count값도 보여준다.
부분 총계

세부 그룹들을 좀 더 큰 단위의 그룹으로 중간중간 합쳐준다.
상위 조건 기준

### 28.
'원래의 NULL'   vs   '부분 총계임을 나타내기 위해 사용된 NULL'
구분방법

## WITH ROLLUP (어렵)
1. GROUP BY 뒤 기준들의 순서에 따라 WITH ROLLUP 의 결과도 달라집니다.
2. NULL임을 나타내기 위해 쓰인 NULL vs. 부분 총계을 나타내기 위해 쓰인 NULL

 애초에 region 컬럼에 NULL이 들어있던 row들의 그룹을 나타내고 있는 것 뿐인데요.

 이 둘을 구분할 수 있게 해주는 함수가 있는데요. 바로 GROUPING이라는 함수

 각 그루핑 기준을 GROUPING이라는 함수의 인자로 넣은 3개의 컬럼들을 추가

 정리하면, GROUPING 함수는,

(1) 실제로 NULL을 나타내기 위해 쓰인 NULL인 경우에는 0,

(2) 부분 총계를 나타내기 위해 표시된 NULL은 1

을 리턴해서 둘을 구분하게 해주는 함수입니다.


## 여러 테이블 조인하기
```sql
SELECT 
    category, 
    main_month, 
    COUNT(*) AS '영화 수', 
    SUM(view_count) AS '총 관객 수'
FROM 2020_movie_report
GROUP BY category, main_month
WITH ROLLUP
HAVING 
    main_month = 5
    AND SUM(view_count) >= 3000000
```

### Foreign Key
 stock 테이블의 item_id 컬럼과 item 테이블의 id 컬럼이 갖는 관계

 Foreign Key는 우리말로 외래키라고도 합니다.

바로 이럴 때

(1) 참조를 하는 테이블인 stock 테이블을 ‘자식 테이블’

(2) 참조를 당하는 테이블인 item 테이블을 ‘부모 테이블’

이라고 합니다. 

 Foreign Key는 다른 테이블의 특정 row를 식별할 수 있어야 하기 때문에 주로 다른 테이블의 Primary Key를 참조할 때가 많습니다. 

Foreign Key 장점: 이상한 값을 추가하려고 할 때 error.

### 다른 종류의 테이블 조인
join: 연결하다, 합치다
```sql
SELECT 
    item.id,
    item.name,
    stock.item.id,
    stock.inventory_count
FROM item LEFT OUTER JOIN stock
ON item.id = stock.item_id
```
//LEFT OUTER JOIN: 왼쪽 기준 (stock)
//RIGHT OUTER JOIN: 오른쪽 기준 (item)

조인할 때 테이블에 alias
```sql
SELECT 
    i.id,
    i.name,
    s.item.id,
    s.inventory_count
FROM item AS i LEFT OUTER JOIN stock AS s
ON item.id = stock.item_id
```
SQL 문 안에서 우리는

컬럼 이름에도 alias를 붙일 수 있고, 

테이블 이름에도 alias를 붙일 수 있습니다.

그리고 둘다 원래 이름 뒤에 AS를 쓰거나, 스페이스 하나를 띄우고 그 뒤에 alias를 쓰면 된다는 점이 같은데요. 

하지만 두 종류의 alias는 약간의 용도 차이가 있습니다. 

일단 컬럼의 alias는 각 컬럼 이름이 실제로 우리에게 그 alias로 변환되어서 보여지게 하기 위한 용도로 쓰입니다. 

이와 달리 테이블의 alias는 조회 결과에서 보기 위한 게 아니라 SQL 문의 전체 길이를 줄여서 가독성을 높이기 위해 사용됩니다. 그리고 특히 조인(join)을 할 때, 만약 서로 다른 테이블에 같은 이름의 컬럼이 존재한다면, SQL 문 안에서 그 컬럼을 가리킬 때 무슨 테이블의 컬럼인지를 더 짧게 표현해주기 위해서도 사용되구요.

```sql
SELECT 
    i.id,
    i.name,
    s.item.id,
    s.inventory_count
FROM item AS i INNER JOIN stock AS s
ON item.id = stock.item_id
```
inner join
: 둘 다 존재하는 것만 합침
기준이 되는 테이블이 따로 없다.

inner join 결과가 다르게 나오는 경우

Foreign Key가 아닌 컬럼을 기준으로 해서 조인
세 가지 조인의 결과가 모두 달라집니다.

Foreign Key가 있을 때, 참조당하는 테이블(referenced table)을 ( 부모 ) 테이블, 참조하는 테이블(referencing table)을 ( 자식 ) 테이블이라고 합니다

SELECT p.name, COALESCE(s.sales_volume, '판매랑 정보 없음') AS '판매량'
FROM pizza_price_cost as p LEFT OUTER JOIN sales as s
ON s.id = p.id

```sql
SELECT p.name, COALESCE(s.sales_volume, '판매량 정보 없음') AS '판매량'
FROM pizza_price_cost AS p LEFT OUTER JOIN sales AS s
ON p.id = s.menu_id;
```

### 결합 연산과 집합 연산
테이블을 합치는 연산은 크게 결합 연산과 집합 연산으로 나눌 수 있습니다.

결합 연산은 테이블을 가로 방향으로 합치는 것에 관한 연산이고,

집합 연산은 테이블을 세로 방향으로 합치는 것에 관한 연산입니다

조인은 결합 연산
집합 연산은 같은 종류의 테이블들끼리만 가능

(1) A ∩ B (INTERSECT 연산자 사용)
SELECT * FROM member_A 

INTERSECT 

SELECT * FROM member_B

(2) A - B (MINUS 연산자 또는 EXCEPT 연산자 사용)
SELECT * FROM member_A 

MINUS

SELECT * FROM member_B

(3) B - A (MINUS 연산자 또는 EXCEPT 연산자 사용)
SELECT * FROM member_B

MINUS

SELECT * FROM member_A

(4) A U B (UNION 연산자 사용)
SELECT * FROM member_A

UNION

SELECT * FROM member_B

### 같은 종류의 테이블 조인
```sql
SELECT 
    old.id,
    old.name,
    new.id,
    new.name
FROM item AS old LEFT OUTER JOIN item_new AS new
ON old.id = new.id
WHERE old.id IS NULL;
```
item -> item_new 이동

LEFT OUTER JOIN, LEFT OUTER JOIN
추가, 삭제 정보 확인

UNION
```sql
SELECT * from item
UNION
SELECT * from item_new;
```

### USING
만약 조인 조건으로 쓰인 두 컬럼의 이름이 같으면 ON 대신 USING을 쓰는 경우도 있습니다.

```sql
SELECT 
    old.id,
    old.name,
    new.id,
    new.name
FROM item AS old LEFT OUTER JOIN item_new AS new
USING(id)
```

### UNION 더 
1. 서로 다른 종류의 테이블도, 조회하는 컬럼을 일치시키면 집합 연산이 가능합니다. 
2. UNION 과 UNION ALL
 교집합에 해당하는 영역의 row들은 중복을 제거하고, 그냥 딱 하나의 row만 보여준다는 겁니다. 이것이 UNION의 특징인데요. 
 이럴 때는 UNION 말고 UNION ALL이라는 연산자를 사용하면 됩니다. UNION ALL은 UNION처럼 두 테이블의 합집합을 보여준다는 점은 같습니다. 하지만 겹치는 것을 중복 제거하지 않고, 겹치는 것들을 그대로 둘다 보여준다는 차이점이 있죠. 이번에는 UNION 대신 UNION ALL 연산을 해보겠습니다.


 ### 3개의 테이블 조인
 ```sql
SELECT 
    i.id,i.name,
    r.item.id, r.star, r.comment, r.mem_id,
    m.id, m.email
FROM 
    item AS i LEFT OUTER JOIN review AS r
        ON r.item_id = i.id
    LEFT OUTER JOIN member AS m
        ON r.mem_id = m.id
```

'상품'과 '리뷰'처럼 1:n 관계인 경우에는 조인을 할 때 1:n 중 1에 해당하는 테이블의 row는 위 그림처럼 조인 결과에서 여러 번 중복 등장할 수 있게 되는 겁니다.

### 의미있는 데이터 추출

여성 중 별점 평균값이 가장 높은 상품
 ```sql
SELECT i.id, i.name, AVG(star), COUNT(*)
FROM 
    item AS i LEFT OUTER JOIN review AS r
        ON r.item_id = i.id
    LEFT OUTER JOIN member AS m
        ON r.mem_id = m.id
where m.gender = 'f'
GROUP BY i.id, i.name
HAVING COUNT(*) > 1
ORDER BY 
    AVG(star) DESC
    COUNT(*) DESC;
```
상품별로 그루핑

별점이 전부 5점? 리뷰 수를 보자. 리뷰 1개 별점 5점.
2개 이상이어야 의미가 있다.

리뷰 낮은 것 조회해보자.
 ```sql
SELECT * FROM review WHERE item_id = 2;
```
 ```sql
SELECT 
    YEAR(i.registration_date) AS '등록 연도',
    COUNT(*) AS '리뷰 개수',
    AVG(star) AS '별점 평균값'
FROM review AS r INNER JOIN item AS i
    ON i.id = r.item_id
        INNER JOIN member AS m 
        ON m.id = r.mem_id
WHERE i.gender = 'u'
GROUP BY YEAR(i.registration_date)
HAVING COUNT(*) >= 10
ORDER BY AVG(star) DESC;
 ```

### 다른 종류의 조인
이때까지 배운 내용을 한번 정리해볼까요?

두 테이블을 서로 합치는 연산에는 크게 두 가지 종류가 있다고 했습니다. 

첫 번째는 두 테이블을 가로 방향으로 합치는 것에 관한 결합 연산, 

두 번째는 두 테이블을 세로 방향으로 합치는 것에 관한 집합 연산 

이라고 했는데요. 

결합 연산 중에서는 LEFT OUTER JOIN, RIGHT OUTER JOIN, INNER JOIN 

집합 연산 중에서는 INTERSECT, MINUS, UNION, UNION ALL

을 배웠습니다. 이때 집합 연산 중 INTERSECT, MINUS 연산자는 MySQL에서 지원하지 않아서, 조인을 통해 간접적으로 원하는 결과를 얻었던 거, 기억나시죠?  
이번 노트에서는 우리가 배우지 않았던 조인 종류들을 배워보겠습니다. 이전에 배운 것들에 비해 실무적으로 활용도는 떨어지지만, 알아두고 있으면 좋은 내용이라서 소개하겠습니다. 혹시라도 현장에서 일을 하다가 이번 노트에서 나온 조인을 들었는데 모르는 상태면 안 될 테니까요. 

하나씩 순서대로 소개하겠습니다. 

1. NATURAL JOIN
NATURAL JOIN은 두 테이블에서 같은 이름의 컬럼을 찾아서 자동으로 그것들을 조인 조건을 설정하고, INNER JOIN을 해주는 조인입니다. 우리말로는 자연 조인이라고도 하는데요.
사실 두 테이블에 같은 이름의 컬럼이 있더라도 NATURAL JOIN을 쓰기보다는 우리가 배운 조인을 쓰고 ON 절에 조인 조건을 명시해주는 것이 좋습니다. NATURAL JOIN을 해버리면 SQL 문을 보더라도, 테이블 구조를 모르는 사람이라면 어떤 컬럼들을 기준으로 조인이 될지 알 수 없으니까요. 하지만 NATURAL JOIN이 사용된 SQL 문을 만나게 되면, 해석할 수 있어야하기 때문에 알려드리는 겁니다.  

2. CROSS JOIN 
CROSS JOIN은 한 테이블의 하나의 row에 다른 테이블의 모든 row들을 매칭하고, 그 다음 row에서도 또, 다른 테이블의 모든 row들을 매칭하는 것을 반복함으로써 두 테이블의 row들의 모든 조합을 보여주는 조인입니다. 잠깐 아래 그림을 보세요.
 Cartesian Product

3. SELF JOIN
SELF JOIN은 셀프라는 단어의 뜻 그대로 테이블이 자기 자신과 조인을 하는 경우를 말합니다.
employee 테이블의 boss 컬럼과 id 컬럼을 기준으로 LEFT OUTER JOIN인 SELF JOIN을 했더니 각 직원 옆에 직속 상사 정보도 함께 뜨죠? 

4. FULL OUTER JOIN
FULL OUTER JOIN은 두 테이블의 LEFT OUTER JOIN 결과와 RIGHT OUTER JOIN 결과를 합치는 조인입니다. 대신, 이때 두 결과에 모두 존재하는 row들(두 테이블에 공통으로 존재하던 row들)은 한번만 표현해주죠.

5. Non-Equi 조인 
등호가 아니라 부등호(<)가 들어있는데요. 

## 서브 쿼리
SQL 안에 부품처럼 들어가는 SELECT문

평균값보다 낮은 별점을 가진 i 찾기
 ```sql
SELECT  i.id, i.name, AVG(star) AS avg_star
FROM item AS i LEFT OUTER JOIN review as r
ON r.item_id = i.id
GROUP BY i.id, i.name
HAVING avg_star < (SELECT AVG(star) FROM review)
ORDER BY AVG(star) DESC;
 ```

sub: 하위, 일브
Query: 데이터베이스에 보내는 요청

괄호고 서브쿼리를 꼭 감싸주어야 함

서브쿼리를 포함하는 전체 SQL 문을 outer query(외부 쿼리), 서브쿼리를 inner query(내부 쿼리)라고 하기도 합니다. 
HAVING 절 뿐만 아니라 SELECT 절, WHERE 절, FROM 절 등에서도 사용할 수 있습니다. 


SELECT절 서브쿼리
 ```sql
SELECT  
    id, 
    name, 
    price,
    (SELECT MAX(price) FROM item) AS max_price
FROM databases.item;
 ```

WHERE절 서브쿼리
 ```sql
SELECT  
    id, 
    name, 
    price,
    (SELECT MAX(price) FROM item) AS max_price
FROM databases.item;
WHERE price > (SELECT AVG(price) FROM item)
 ```
```sql
SELECT  
    id, 
    name, 
    price,
FROM databases.item;
WHERE price = (SELECT MAX(price) FROM item)
 ```

값을 여러 개 return하는 서브쿼리
리뷰가 최소 3개 이상 달린 상품들의 정보만 보고 싶음
```sql
SELECT * FROM databases.item
WHERE id IN
{
    SELECT item_id
    FROM review
    GROUP BY item_id HAVING COUNT(*) >= 3
};
 ```

 IN을 붙여서 유용하게 사용했는데요. IN 말고도 이런 서브쿼리와 함께 유용하게 사용되는 다른 키워드들도 있습니다. 

바로 ANY와 ALL이라는 것인데요. 하나씩 배워볼게요.
1. ANY의 의미
하나라도 조건을 만족하는 경우가 있으면 True를 리턴
단 하나의(ANY) 값보다도 크다면 True를 리턴

. SOME은 '어떤 하나의~' 라는 뜻을 가진 영어 단어죠? SOME도 서브쿼리의 결과에 있는 각 row의 값들 중 하나라도 조건을 만족하면 True를 리

2. ALL의 의미
ALL은 모든 경우에 대해서 해당 조건이 성립해야 True를 리턴

SELECT SUBSTRING(address, 1, 2) FROM member GROUP BY SUBSTRING(address, 1, 2) ORDER BY COUNT(*) DESC LIMIT 1;

이 서브쿼리는

(1) 주요 지역별로 회원들을 그루핑한 후에,

(2) 그룹들을 각 그룹당 row 개수대로 내림차순 정렬하고,

(3) 그 중에서도 1등만 추립니다.


from절 서브쿼리
```sql
SELECT 
    AVG(review_count),
    MAX(review_count),
    MIN(review_count)
FROM
(SELECT  
    SUBSTRING(address, 1, 2) AS region,
    COUNT(*) AS review_count
FROM review AS r LEFT OUTER JOIN member AS m 
ON r.mem_id = m.id
GROUP BY SUBSTRING(address, 1, 2)
HAVING region IS NOT NULL
    AND region != '안드') AS review_count_summary;
 ```
 서브쿼리 테이블 = derived table
 생성할 떄 꼭 alias를 붙여주어야 한다.

 ### 서브쿼리의 종류 총정리
 1. 단일값을 리턴하는 서브쿼리
 스칼라 서브쿼리라고도 합니다. 이런 스칼라 서브쿼리는 SELECT 절에서 하나의 컬럼처럼, WHERE 절에서 =, > 등의 조건 표현식과 비교하는 값으로 쓸 수 있겠죠? 
 2. 하나의 column에 여러 row들이 있는 형태의 결과를 리턴하는 서브쿼리 
IN, ANY(SOME), ALL 등의 키워드와 함께 쓸 수 있다고 했던 거, 기억나시죠? 
3. 하나의 테이블 형태의 결과(여러 column, 여러 row)를 리턴하는 서브쿼리 
derived table이라고 한다고 했죠?(Oracle에서는 inline view라고도 합니다) 이런 서브쿼리로 생겨난 derived table은 마치 원래 있던 테이블인 것처럼 사용하면 됩니다. 대신, derived table에는 alias를 붙여줘야 한다는 규칙이 있습니다. 

서브쿼리를 

(1) 비상관 서브쿼리와

(2) 상관 서브쿼리로

이 서브쿼리가 그것을 둘러싼 outer query와 별개로, 독립적으로 실행되기 때문
이렇게 outer query와 상관 관계가 없는 서브쿼리를 비상관 서브쿼리라고 합니다. 이때까지 우리가 배운 서브쿼리들이 모두 비상관 서브쿼리에 해당합니다. 

상관 서브쿼리란 outer query와 상관 관계가 있는 서브쿼리를 말하는데요. 아래 예시와 함께 설명할게요. 
서브쿼리가 outer query에 적힌 테이블 이름 등과 상관 관계를 갖고 있어서 그 단독으로는 실행되지 못하는 서브쿼리를 상관 서브쿼리라고 합니다. 

```sql
SELECT * FROM item
    WHERE NOT EXISTS (SELECT * FROM review WHERE review.item_id = item.id)
 ```
EXISTS
NOT EXISTS

EXISTS 없이 사용하는 방법
```sql
SELECT *,
(SELECT MIN(height)
 FROM member AS m2 WHERE birthday IS NOT NULL AND height IS NOT NULL
 AND YEAR(m1.birthday) = YEAR(m2.birthday)) AS min_height_in_the_year
 FROM member AS m1
 ORDER BY min_height_in_the_year ASC;
 ```

 SELF JOIN 같은 작업
 비상관 서브쿼리는 영어로 Non-correlated Subquery, 상관 서브쿼리는 영어로 Correlated Subquery

 ### 서브쿼리 vs 조인

그럼 과연 상관 서브쿼리와 조인, 이 둘 중에서 무엇을 써야할까요? 정답은 없습니다. 데이터를 분석할 때는 여러분이 더 익숙하고 직관적으로 이해할 수 있는 것을 선택하면 되는데요.

### 서브쿼리로 더 간결해진 CASE함수
```sql
SELECT 
    BMI,
(CASE
    WHEN BMI>=25 THEN '비만'
    ELSE '체중'
END) AS obsity_check

FROM
(SELECT weight / ((height/100)*(height/100)) AS BIM FROM databases.member) AS subquery_for_BMI
 ```

 ### 서브쿼리의 중첩과 그 문제점

 서브쿼리 안 서브쿼리
 ```sql
 SELECT  
    i.id, 
    i.name, 
    AVG(star) AS avg_star,
    COUNT(*) AS count_star
FROM item AS i LEFT OUTER JOIN review AS r 
    ON r.item_id = i.id
        LEFT OUTER JOIN member AS m
        ON r.mem_id = m.id
WHERE m.gender = 'f'
GROUP BY i.id, i.name
 HAVING COUNT(*) >= 2 AND avg_star =
 (
    SELECT MAX(avg_star) FROM (
        SELECT  
            i.id, 
            i.name, 
            AVG(star) AS avg_star,
            COUNT(*) AS count_star
        FROM item AS i LEFT OUTER JOIN review AS r 
            ON r.item_id = i.id
                LEFT OUTER JOIN member AS m
                ON r.mem_id = m.id
        WHERE m.gender = 'f'
        GROUP BY i.id, i.name
        HAVING COUNT(*) >= 2
        ORDER BY AVG(star) DESC, COUNT(*) DESC
    ) AS final
 )
 ORDER BY AVG(star) DESC, COUNT(*) DESC;
 ```
 가장 안과 가장 밖(final table) 같은 내용
 중첩해서 사용하면 너무 길어져서 읽기 힘들어짐. 중복되는 부분도 있음
 간편한 방법이 있다!

 ### 뷰
 뷰: 조인 등의 작업을 해서 만든 '결과 테이블'이 가상으로 저장된 형태
 CREATE VIEW '뷰 이름' AS SELECT 문;을 사용하면 뷰를 생성할 수 있습니다.
  ```sql
CREATE VIEW three_tables_joied AS
SELECT  
    i.id, 
    i.name, 
    AVG(star) AS avg_star,
    COUNT(*) AS count_star
FROM item AS i LEFT OUTER JOIN review AS r 
    ON r.item_id = i.id
        LEFT OUTER JOIN member AS m
        ON r.mem_id = m.id
WHERE m.gender = 'f'
GROUP BY i.id, i.name
HAVING COUNT(*) >= 2
ORDER BY AVG(star) DESC, COUNT(*) DESC
 ```
  ```sql
SELECT  * FROM databases.three_tables_joined
WHERE avg_star = (
    SELECT MAX(avg_star) FROM databases.three_tables_joined
) AND count_star = (
    SELECT MAX(count_star) FROM databases.three_tables_joined
);
 ```
 첫 번째, 뷰는 사용자에게 높은 편의성을 제공해줍니다. 
 두 번째, 각 직무별 데이터 수요에 알맞은, 다양한 구조의 데이터 분석 기반을 구축해둘 수 있습니다. 
 세 번째, 뷰는 데이터 보안을 제공합니다. 

 ### 데이터확인
 SHOW DATABASES;
 SHOW FULL TABLES IN databases;
 DESCRIBE item; //컬럼 구조 파악
 외래키 파악
 WHERE i.CONSTRAINT_TYPE = 'FOREIGN KEY'

서브쿼리 기초 과제
 SELECT * FROM review
WHERE item_id IN
(SELECT id FROM item 
WHERE YEAR(registration_date) <= 2018)

서브쿼리 종합 과제
SELECT 
    MAX(copang_report.price) AS max_price,
    AVG(copang_report.star) AS avg_star,
    COUNT(DISTINCT(copang_report.email)) AS distinct_email_count
FROM 
(
  SELECT  price,email,star
  FROM review AS r INNER JOIN member AS m
  ON r.mem_id = m.id
  INNER JOIN item AS i
  ON r.item_id = i.id
) AS copang_report;

CREATE VIEW v_emp AS
(SELECT id,name,age,department,phone_num,hire_date
FROM employee);
SELECT * FROM v_emp;
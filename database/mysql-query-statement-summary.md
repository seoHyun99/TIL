# [Database] MySQL 쿼리 정리

- CREATE DATABASE *database*  
→ database란 이름을 가진 데이터베이스 생성

- USE *database*  
→ database를 사용

- DESC *table*  
→ 테이블 정의 출력

#### SHOW
- SHOW *databases*  
→ 현재 서버의 데이터베이스 출력

- SHOW *tables*  
→ 현재 데이터베이스의 테이블 출력

- SHOW INDEX FROM *a_table*  
→ A 테이블의 인덱스 출력

- SHOW COLUMNS FROM *a_table*  
→ A 테이블의 구조 출력

- SHOW CREATE TABLE *a_table*  
→ A 테이블 생성 SQL문 출력

#### SELECT
- SELECT COUNT(*) FROM *a_table*  
→ A 테이블의 row 수 출력

- SELECT * FROM *a_table*  
→ A 테이블에 있는 모든 column 출력

- SELECT *a_column* FROM *a_table*  
→ A 테이블에 있는 A column 출력

- SELECT *a_column* FROM *a_table* WHERE *a_column = 1*  
→ A 테이블에 있는 A column 중 값이 1인 데이터만 출력

- SELECT DISTINCT *a_column* FROM *a_table* WHERE *a_column = 1*  
→ A 테이블에 있는 A column의 데이터가 중복하지 않으면서 값이 1인 데이터만 출력

- SELECT * FROM *a_table* ORDER BY *a_column* ASC  
→ A 테이블에 있는 데이터를 A column을 기준으로 오름차순 정렬 / ASC 생략 가능

- SELECT * FROM *a_table* ORDER BY *a_column* DESC  
→ A 테이블에 있는 데이터를 A column을 기준으로 내림차순 정렬

- SELECT * FROM *a_table* WHERE *a_column* LIKE 'b%'  
→ A 테이블에 있는 데이터 중 A column의 값이 b로 시작되는 row 출력

- SELECT * FROM *a_table* WHERE *a_column* LIKE '%b'  
→ A 테이블에 있는 데이터 중 A column의 값이 b로 끝나는 row 출력

- SELECT * FROM *a_table* WHERE *a_column* LIKE '%b%'  
→ A 테이블에 있는 데이터 중 A column의 값이 b를 포함하는 row 출력

- SELECT * FROM *a_table* WHERE *a_column* REGEXP '^.....$'  
→ A 테이블에 있는 A column 중 5문자인 row 출력

- SELECT * FROM *a_table* WHERE LENGTH(*a_column*) = 5  
→ A 테이블에 있는 A column 중 5문자인 row 출력

- SELECT *a_column* FROM *a_table* LIMIT 10  
→ A 테이블에 있는 A column을 처음부터 10개 출력

- SELECT *a_column* FROM *a_table* LIMIT 10, 5  
→ A 테이블에 있는 A column을 10번째부터 5개 출력

- SELECT AVG(*a_column*), MIN(*a_column*), MAX(*a_column*), SUM(*a_column*) FROM *a_table*  
→ A 테이블에 있는 A column의 평균, 최소, 최대, 합계 출력  
→ AVG : 평균값 / MIN : 최소값 / MAX : 최대값 / SUM : 평균

- SELECT *a_column* FROM *a_table* UNION SELECT *b_column* FROM *b_table*  
→ A 테이블과 B 테이블에서 A column과 B column 모든 값을 한 번에 출력

#### UPDATE
- UPDATE *a_table* SET *a_column*='a' WHERE *b_column* > 0  
→ A 테이블에 있는 B column의 값이 0보다 클 경우 A column의 값을 A로 변경

- UPDATE *a_table* SET *a_column*=TRIM(*a_column*)  
→ A 테이블에 있는 A column의 왼쪽, 오른쪽 공백 제거

#### INSERT
- INSERT INTO *a_table*(*a_column, b_column*) VALUES ('A', 'B')  
→ A 테이블에 A column에 A, B column에 B를 넣음

#### ALTER
- ALTER TABLE *a_table* ADD *a_column* *data_type*  
→ A 테이블에 해당 데이터 타입의 A column 추가

- ALTER TABLE *a_table* DEL *a_column*  
→ A 테이블의 A column 제거

- ALTER TABLE *a_table* MODIFY *a_column* *data_type*   
→ A 테이블의 A column을 해당 데이터 타입으로 변환

- ALTER TABLE *a_table* CHANGE *old_column* *new_column* *data_type*  
→ A 테이블의 column명과 데이터 타입 변경

- ALTER TABLE *a_table* TYPE = *TYPE(EX.innodb)*  
→ A 테이블의 타입을 해당 타입으로 변경


#### 날짜, 시간 관련
- SELECT NOW()  
→ 현재 날짜와 시간 출력

- SELECT SYSDATE()  
→ 현재 날짜와 시간 출력

- SELECT CURDATE()   
→ 현재 날짜 출력

- SELECT CURTIME()   
→ 현재 시간 출력

- SELECT UNIX_TIMESTAMP()  
→ '1970-01-01 00:00:00'으로부터 경과한 시간을 초단위로 출력

- SELECT DAYOFWEEK('*XXXX-XX-XX*')  
→ 해당 날짜의 요일을 숫자로 출력 (1: 일요일 ~ 7: 토요일)

- SELECT WEEKDAY('*XXXX-XX-XX*')  
→ 해당 날짜의 요일을 숫자로 출력 (0: 월요일 ~ 6: 일요일)

- SELECT DAYOFYEAR(*NOW()*)  
→ 해당 날짜의 1월 1일부터 경과 일수 출력

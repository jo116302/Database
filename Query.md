공부하면서 실습 및 참고할 수 있는 사이트
- [참고 링크1](https://sqltest.net/#)
- [참고 링크2](https://livesql.oracle.com/apex/livesql/file/tutorial_D39T3OXOCOQ3WK9EWZ5JTJA.html)

<hr />

> # [기본적인 쿼리 구문](https://server-talk.tistory.com/159)

>> ## DDL

- 데이터베이스를 정의하는 언어, 데이터리를 생성/수정/삭제하는 등의 데이터의 전체의 설정

>> ## DML

- 데이터베이스에 입력된 레코드를 조회/수정/삭제 등의 역할 수행하는 언어

>>> ### SELECT

- Query문 구조
  ```sql
  SELECT [COLUMN_NAME OR *] FROM [TABLE_NAME] [WHERE 조건]
  ```

>>> ### INSERT

- Query문 구조
  ```sql
  INSERT INTO [TABLENAME] ([입력을 원하는 COLUMN]...) VALUES ([해당 COLUMN에 입력할 값]...);
  ```

>>> ### UPDATE

- Query문 구조
  ```sql
  UPDATE [tableName] SET [columnName] = [변경할 값] WHERE [조건];
  ```

>>>> #### field value의 수정사항

- **UPDATE** 문 사용
- 개행 제거
  - [Query문 구조](https://curryyou.tistory.com/68)
    ```sql
    UPDATE [tableName] SET [fieldName] = REPLACE([fieldName], '\r\n', '');
    ```

>>> ### DCL

- 데이터베이스에 접근 또는 객체에 권한을 주는등의 역할을 하는 언어

> # 테이블이 멀티키 구조 형태일 경우

>> ## PRIMARY KEY 값을 조합하여 UNIQUE 한 값 추출

- 각 PRIMARY KEY로 비교 기준을 삼는다면 중복값이 발생하기 떄문에 이를 방지하기 위하여 PRIMARY KEY에 속하는 모든 값을 조합하여 UNIQUE 값 생성

- 예제 테이블
  | grade | name      | score |
  |:-----:|:-----:|:-----:|
  |     3 | 강한나    |   100 |
  |     2 | 안철수    |   100 |
  |     3 | 김철수    |    80 |
  |     1 | 김재수    |    35 |

>>> ### MySQL
- `concat()` : 한 row 씩 기입된 column을 결합
  ```sql
  select concat([column]...) ... from [TableName]
  ```
- `group_concat()` : 모든 기입된 column을 하나의 row로 출력
  ```sql
  select group_concat([column]...) ... from [TableName]
  ```
- 예제로 출력해보기
  - `concat()`
    ```sql
    select concat(grade, '. ', name, ': ', score) AS Student_Info from student;
    ```
    - 출력 결과
      | Student_Info      |
      |:-----------------|
      | 3. 강한나: 100    |
      | 2. 안철수: 100    |
      | 3. 김철수: 80     |
      | 1. 김재수: 35     |
  - `group_concat()`
    ```sql
    select group_concat(grade, '. ', name, ': ', score) AS Student_Info from student;
    ```
    - 출력 결과 
      | Student_Info                                                        |
      |:--------------------------------------------------------------------|
      | 3. 강한나: 100,2. 안철수: 100,3. 김철수: 80,1. 김재수: 35             |

>>> ### Oracle
- `concat()` : MySQL과 다른 점은 `CONCAT(PARA1, PARA2)` 와 같이 파라미터를 2개까지만 받아 적용할 수 있음
  ```sql
  select concat([Para1], [Para2]) ... from [TableName]
  ```
- `||` : 결합하고 싶은 column 또는 문자열 사이에 붙임자로 넣음
  ```sql
  select [columnName1] || [columnName2] from [TableName]
  ```
- 예제로 출력해보기
  - `concat()`
    - 1번 예제 
    ```sql
    select concat(grade, name) from student;
    ```
    - 결과물
      | Student_Info      |
      |:-----------------|
      | 3강한나    |
      | 2안철수    |
      | 3김철수     |
      | 1김재수     |
    - 2번 예제
    ```sql
    select concat(concat(grade, '. '), name) from student;
    ```
    - 결과물
      | Student_Info      |
      |:-----------------|
      | 3. 강한나    |
      | 2. 안철수    |
      | 3. 김철수     |
      | 1. 김재수     |
  - `||`
    ```sql
    select grade ||'. '|| name ||': '|| score from student;
    ```
    - 결과물
      | Student_Info      |
      |:-----------------|
      | 3. 강한나: 100    |
      | 2. 안철수: 100    |
      | 3. 김철수: 80     |
      | 1. 김재수: 35     |

> # Value Check and Input

1) NVL()
  - 필드에 값의 유무(NULL)를 확인
  - 사용 함수 [`NVL`](https://docs.oracle.com/cd/B19306_01/server.102/b14200/functions105.htm#i91798)
    - NVL([value1], [value2])
    - 첫 파라미터 인자값이 NULL이면, 두번째 인자값으로 대체

2) CASE WHEN
  - 특정 값인지 확인 (IF 문법)
  - 사용 함수
    ```sql
    CASE WHEN [조건1] THEN [참일 경우 값1]
         WHEN [조건2] THEN [참일 경우 값2]
         ...
         ELSE [조건문에 걸러지지 않은 값]
    END
    ```

>> ## 예제로 확인

- 예제를 위한 테이블과 값 저장
  ```sql
  CREATE TABLE sql_test_a ( 
      ID         VARCHAR2(4000 BYTE), 
      FIRST_NAME VARCHAR2(200 BYTE), 
      LAST_NAME  VARCHAR2(200 BYTE) 
  );
  
  INSERT INTO sql_test_a (ID, FIRST_NAME, LAST_NAME) VALUES ('1', 'John', 'Snow'); 
  INSERT INTO sql_test_a (ID, FIRST_NAME, LAST_NAME) VALUES ('2', 'Mike', 'Tyson'); 
  INSERT INTO sql_test_a (ID, FIRST_NAME, LAST_NAME) VALUES ('3', 'Bill', 'Keaton'); 
  INSERT INTO sql_test_a (ID, FIRST_NAME, LAST_NAME) VALUES ('4', 'Greg', 'Mercury'); 
  INSERT INTO sql_test_a (ID, FIRST_NAME, LAST_NAME) VALUES ('5', 'Steve', 'Jobs'); 
  INSERT INTO sql_test_a (FIRST_NAME, LAST_NAME) VALUES ('Johhny', 'Depp');
  INSERT INTO sql_test_a (FIRST_NAME, LAST_NAME) VALUES ('Jonly', 'Wang');
  ```
1) NVL()
  - NVL를 사용하지 전 조회 값
    ```sql
    SELECT 
      NVL(ID, 'NO_ID'),
      FIRST_NAME,
      LAST_NAME
    FROM sql_test_a;
    ```

    - 결과
      |ID | FIRST_NAME | LAST_NAME|
      |:-:|:-:|:-:|
      |1	|John|	Snow|
      |2	|Mike|	Tyson|
      |3	|Bill|	Keaton|
      |4	|Greg|	Mercury|
      |5	|Steve|	Jobs|
      ||	Johhny|	Depp|
      ||	Jonly|	Wang|

  - NVL를 사용 후 조회 값
    ```sql
    SELECT 
        NVL(ID, 'NO ID') AS ID,
        FIRST_NAME,
        LAST_NAME
    FROM sql_test_a;
    ```
    - 결과
      |ID | FIRST_NAME | LAST_NAME|
      |:-:|:-:|:-:|
      |1	|John|	Snow|
      |2	|Mike|	Tyson|
      |3	|Bill|	Keaton|
      |4|Greg|	Mercury|
      |5|Steve|	Jobs|
      |NO_ID|	Johhny|	Depp|
      |NO_ID|	Jonly|	Wang|

2) CASE WHEN
  - 조건문을 사용한 조회 쿼리
    ```sql
    SELECT 
      CASE WHEN ID='1' THEN 'ONE'
           WHEN ID='2' THEN 'TWO'
           WHEN ID='3' THEN 'THREE'
           WHEN ID='4' THEN 'FOUR'
           WHEN ID='5' THEN 'FIVE'
           ELSE 'EMPTY'
      END AS ID,
      FIRST_NAME,
      LAST_NAME
    FROM sql_test_a;
    ```
    - 결과
      |ID | FIRST_NAME | LAST_NAME|
      |:-:|:-:|:-:|
      |ONE	|John|	Snow|
      |TWO	|Mike|	Tyson|
      |THREE	|Bill|	Keaton|
      |FOUR|Greg|	Mercury|
      |FIVE|Steve|	Jobs|
      |EMPTY|	Johhny|	Depp|
      |EMPTY|	Jonly|	Wang|

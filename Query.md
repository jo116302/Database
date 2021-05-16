공부하면서 실습 및 참고할 수 있는 사이트
- [참고 링크1](https://sqltest.net/#)

<hr />

> # 기본적인 쿼리 구문

>> ## UPDATE

- Query문 구조
  ```sql
  UPDATE [tableName] SET [columnName] = [변경할 값] WHERE [조건]
  ```

> # field value의 수정사항

- **UPDATE** 문 사용
- 개행 제거
  - [Query문 구조](https://curryyou.tistory.com/68)
    ```sql
    UPDATE [tableName] SET [fieldName] = REPLACE([fieldName], '\r\n', '');
    ```

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

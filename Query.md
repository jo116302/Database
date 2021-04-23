> # 기본적인 쿼리 구문

>> ## UPDATE

- Query문 구조
  ```sql
  UPDATE [tableName] SET [columnName] = [변경할 값] WHERE [조건]
  ```

> # field value의 수정사항

- **UPDATE** 문 사용
- 개행 제거
  - Query문 구조
    ```sql
    UPDATE [tableName] SET [fieldName] = REPLACE([fieldName], '\r\n', '');
    ```

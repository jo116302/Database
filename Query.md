> # 기본적인 쿼리 구문

>> ## UPDATE

- `UPDATE [tableName] SET [columnName] = [변경할 값] WHERE [조건]`

> # field value의 수정사항

- **UPDATE** 문 사용
- 개행 제거
  - `update [tableName] set [fieldName] = replace([fieldName], '\r\n', '');

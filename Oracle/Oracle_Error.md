> # Oracle Connection Error

>> ## ORA-28040: No matching authentication protocol

- [참고 링크1](http://www.koreaoug.org/security/7837)
- 12C 버전 이후로는 알파벳 대소문자 및 접속 인증 프로토콜 버전이 암호화됨에 따라 Client에서 못붙는 경우
- 프로토콜 문제로 접속 않되는 문제
  - `$ORACLE_HOME/network/admin/sqlnet.ora` 수정
    ```ora
    NAME.DIRECTORY_PATH= (TNSNAMES, ONAMES, HOSTNAME, EZCONNECT)
    SQLNET.ALLOWED_LOGON_VERSION_SERVER=[유저 패스워드 방식을 서버단에서 변경을 준비]
    SQLNET.ALLOWED_LOGON_VERSION_CLIENT=[클라이언트 버전이 낮아도 접속을 허용]
    ```
- 접속 계정 패스워드 변경
  ```sql
  ALTER USER [ACCOUNT_NAME] IDENTIFIED BY [PASSWORD];
  ```

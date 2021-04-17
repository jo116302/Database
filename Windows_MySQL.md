> # MySQL CharacterSet 변경
 
- 한글로 타입 변경
  - `C:\Program Files\MySQL\MySQL Server 5.1\my.ini` 경로 파일 수정
    ```ini
    [client]
    default-character-set=utf8
    
    [mysqld]
    character-set-client-handshake = FALSE
    init_connect="SET collation_connection = utf8_general_ci"
    init_connect="SET NAMES utf8"
    character-set-server = utf8
    ```

- 만약 언어 타입에 문제가 있다고 출력되는 경우 `C:\Program Files\MySQL\MySQL Server 5.1\share\charsets\index.xml` 확인하기
  - 지원하는 언어 타입이 존재여부 확인할 것
  - 언어 타입이 존재한다면 `name`이 설정과 같은지 확인
    ```xml
    <charset name="utf8">
      <family>Unicode</family>
      <description>UTF-8 Unicode</description>
      <alias>utf-8</alias>
      <collation name="utf8_general_ci"	id="33">
        <flag>primary</flag>
        <flag>compiled</flag>
      </collation>
      <collation name="utf8_bin"		id="83">
        <flag>binary</flag>
        <flag>compiled</flag>
      </collation>
    </charset>
    ```

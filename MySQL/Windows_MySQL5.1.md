> # Archives version 설치

- 다운로드 링크 : https://downloads.mysql.com/archives/community/
- 환경변수 잡아주기
  - `MySQL_HOME` 경로 만들기<br /> ![image](https://user-images.githubusercontent.com/81629923/123509409-4c711680-d6b0-11eb-8aca-b0e6bc60b103.png)
  - `MySQL_HOME\bin\`을 Path에 등록하기<br /> ![image](https://user-images.githubusercontent.com/81629923/123509444-8f32ee80-d6b0-11eb-8f6c-0eea6168a2c7.png)
- cmd를 실행시켜 작업하기
  - MySQL 초기화 시키기, `MySQL_HOME` 내에 data 폴더 생성되면 정상적으로 실행된 것으로 봐도 됨
    ```cmd
    mysqld initialize-insecure
    ```
  - 서비스에 MySQL 등록
    ```cmd
    mysqld -install
    ```
    ![image](https://user-images.githubusercontent.com/81629923/123509592-521b2c00-d6b1-11eb-8df2-6bdca6b4d8c5.png)
  - 서비스 실행
    ```cmd
    net start mysql 
    ```
  - MySQL 실행
    - `Enter password`는 기입하지 않고 그냥 Enter
    ```cmd
    mysql -u root -p
    ```
  - ROOT 계정 비밀번호 변경한 후 이용
- [참고 링크1](https://javacpro.tistory.com/70)<br />[참고 링크2](https://coozplz.me/2011/11/10/mysql-%EC%84%9C%EB%B9%84%EC%8A%A4-%EB%93%B1%EB%A1%9D/)


> # MySQL CharacterSet 변경 ([참고](https://lazymankook.tistory.com/70))
 
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

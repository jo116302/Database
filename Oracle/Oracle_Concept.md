> # Basic Concept

>> ## Service Name

- 서버관련, 클라이언트에서 사용하고자 하는 명칭
- Oracle로 접속하기 위해서는 서버IP, 오라클 SID, 접속 프로토콜와 같은 정보 필요
- 위 정보를 묶은 것이 Service Name이며, 서비스 명으로 접속하는데 필요
- [참고 링크1](https://sk-christine.tistory.com/22)

>> ## SID

- 오라클 DB가 설치되어 있는 곳에서 생성한 DB명
- 인스턴스가 서버 역할을 하는 DBMS 프로세스이며, 인스턴스가 기동할 때 SID 필요
- 하나의 서버 내에 다수의 인스턴스 가동이 가능하며, SID로 구별
- `listener.ora`에 설정되어 있음

> # Oracle Setting File

>> ## Listener

- 파일명 : `listener.ora`
- 경로 확인 : `# lsnrctl status`
- Default Path : `$ORACLE_HOME/network/admin/listener.ora`
- 파일 기능 : client가 Oracle server에 접속하기 위해서 server 컴퓨터에 하는 설정 파일
- [참고 링크3](https://sarc.io/index.php/oracledatabase/186-2014-06-10-01-33-05)<br />[참고 링크2](https://docs.oracle.com/database/121/NETRF/listener.htm#NETRF400)<br />[참고 링크3](https://positivemh.tistory.com/563)

>> ## tnsnames

- 파일명 : `tnsnames.ora`
- 경로 확인 :
- Default Path : `$ORACLE_HOME/network/admin/tnsnames.ora`
- 파일 기능 : Oracle server에 접속할 때 필요한 정보들을 설정하는 파일
- [참고 링크3](https://sarc.io/index.php/oracledatabase/186-2014-06-10-01-33-05)<br />[참고 링크2](https://docs.oracle.com/database/121/NETRF/listener.htm#NETRF400)<br />[참고 링크3](https://positivemh.tistory.com/563)

> # Oracle Client

- Oracle Server에 접속하기 위해서 Oralce에서 지원하는 서버와의 연결 툴

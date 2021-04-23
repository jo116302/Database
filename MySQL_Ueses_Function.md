> # SQL 파일 Import/Export

- [참고 링크1](https://bozeury.tistory.com/entry/mysql-%EC%BD%98%EC%86%94%EC%97%90%EC%84%9C-sql-%ED%8C%8C%EC%9D%BC-%EB%82%B4%EB%B3%B4%EB%82%B4%EA%B8%B0)

>> ## SQL 파일 Import

- 1번째 방법 : mysql -u[아이디] -p [데이터베이스명] < [SQL파일경로]
- 2번째 방법 : 사용할 Database 접속 (ex) use Test), source [SQL FilePath]

>> ## SQL 파일 Export

- 1번째 방법 : mysql -u[아이디] -p[패스워드] database > [저장될 파일명]

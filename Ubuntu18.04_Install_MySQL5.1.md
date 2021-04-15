> MySQL 다운로드
  - [참고 깃허브](https://gist.github.com/huangqiheng/7fbfcd7f4f97255447713ec6e9e85257)
  - [다운로드 링크](https://downloads.mysql.com/archives/community/)
    ```
    # wget http://dev.mysql.com/get/Downloads/MySQL-5.1/mysql-5.1.73.tar.gz
    ```
 
 > 압축 풀기 및 설치
   - 압축 풀기 및 설치
     ```
     # apt-get update
     # apt-get install -y build-essential
     # apt-get install -y libncurses5-dev
     # tar xvf mysql-5.1.73.tar.gz
     # cd mysql-5.1.73
     # ./configure \
        '--prefix=/usr' \
        '--exec-prefix=/usr' \
        '--libexecdir=/usr/sbin' \
        '--datadir=/usr/share' \
        '--localstatedir=/var/lib/mysql' \
        '--includedir=/usr/include' \
        '--infodir=/usr/share/info' \
        '--mandir=/usr/share/man' \
        '--with-system-type=debian-linux-gnu' \
        '--enable-shared' \
        '--enable-static' \
        '--enable-thread-safe-client' \
        '--enable-assembler' \
        '--enable-local-infile' \
        '--with-fast-mutexes' \
        '--with-big-tables' \
        '--with-unix-socket-path=/var/run/mysqld/mysqld.sock' \
        '--with-mysqld-user=mysql' \
        '--with-libwrap' \
        '--with-readline' \
        '--with-ssl' \
        '--without-docs' \
        '--with-extra-charsets=all' \
        '--with-plugins=max' \
        '--with-embedded-server' \
        '--with-embedded-privilege-control' \
        CXXFLAGS="-Wno-narrowing -fpermissive"
     
     // make란? - 파일 간의 종속관계를 파악하여 Makefile(기술파일)에 적힌 대로 컴파일러에 명령하여 SHELL 명령 순차적으로 실행
     # make
     // make install란? - make를 통해 만들어진 설치파일(setup)을 설치를 하는 과정
     # make install
     # mkdir -p /etc/mysql
     # mkdir -p /var/lib/mysql
     # mkdir -p /etc/mysql/conf.d
     # cp /usr/share/mysql/my-medium.cnf /etc/mysql/my.cnf
     # sed -i 's#.*datadir.*#datadir = /var/lib/mysql#g' /etc/mysql/my.cnf
     # chown mysql:mysql -R /var/lib/mysql
     
     # mysql_install_db --user=mysql
     # mysqld_safe -user=mysql &
     # /usr/bin/mysql_secure_installation
     
     # cp /usr/share/mysql/mysql.server /etc/init.d/mysql
     # chmod +x /etc/init.d/mysql
     # mysql -u root -p
     ```

> 언어 타입 설정
- 현재 타입 확인
  ```
  # mysql -u root -p
  # status
  # show variables like '%char%';
  ```
- 언어 타입 변경 `# vi /etc/my.cnf`
  ```
  [client] 
  default-character-set = utf8 

  [mysqld] 
  character-set-client-handshake=FALSE 
  init_connect="SET collation_connection = utf8_general_ci" 
  init_connect="SET NAMES utf8" 
  character-set-server = utf8 
  collation-server = utf8_general_ci 

  [mysqldump] 
  default-character-set = utf8 

  [mysql] 
  default-character-set = utf8
  ```
- 수정 반영
  ```
  # sudo service mysql restart
  ```

> 1. Linux X Window 설치

   - 리눅스 별로 X Window 설치 명령어가 상이

   - 리눅스 확인하기

     ```
     # cat /etc/os-release
     ```

- CentOS 7인 경우

  ```
  # sudo yum update
  # sudo yum groupinstall "GNOME Desktop" "Graphical Administration Tools"
  # sudo ln -sf /lib/systemd/system/runlevel5.target /etc/systemd/system/default.target
  # sudo password
  ```

  

> 2. Linux에 MySQL 5.1 설치

- MySQL Download 사이트에서 MySQL 다운
  ![image](https://user-images.githubusercontent.com/81629923/113016748-be24eb80-91b9-11eb-9b16-01b8fc192c08.png)
  - TAR Archive Download 마우스 오른쪽 클릭하여 "Copy Link Location" 선택

    ```
    # groupadd mysql
    # useradd -g mysql mysql
    # wget https://downloads.mysql.com/archives/get/p/23/file/mysql-5.1.73-linux-x86_64-glibc23.tar.gz
    ```

- MySQL 압축 풀기 및 설치

  ```
  # tar xvf mysql-5.1.73-linux-x86_64-glibc23.tar.gz
  # cd mysql-5.1.73-linux-x86_64-glibc23/
  # chown -Rf mysql.mysql .
  ```

  

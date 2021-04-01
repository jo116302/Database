
> 1. Linux X Window 설치

   - 리눅스 별로 X Window 설치 명령어가 상이

   - 리눅스 확인하기

     ```
     # cat /etc/os-release
     ```

- CentOS 7인 경우

  ```
  // X Window 설치
  # sudo yum update
  # sudo yum groupinstall "GNOME Desktop" "Graphical Administration Tools"
  # sudo ln -sf /lib/systemd/system/runlevel5.target /etc/systemd/system/default.target
  # sudo passwd
  
  // Window의 RDP로 접속하기 위한 설치
  # yum install epel-release -y
  # yum -y install xrdp tigervnc-server
  # systemctl enable xrdp.service
  # firewall-cmd --permanent --zone=public --add-port=3389/tcp
  # sudo reboot
  ```

  

> 2. Linux에 MySQL 5.1 설치

- MySQL Download 사이트에서 MySQL 다운([설치 링크](https://downloads.mysql.com/archives/community/))
  ![image](https://user-images.githubusercontent.com/81629923/113018076-1c060300-91bb-11eb-968c-23af29a87b55.png)
  - TAR Archive Download 마우스 오른쪽 클릭하여 "Copy Link Location" 선택

    ```
    # groupadd mysql
    # useradd -g mysql mysql
    // TAR가 아닌 다른 형태의 설치 방법을 사용해도 됨
    # wget https://downloads.mysql.com/archives/get/p/23/file/MySQL-5.1.73-1.glibc23.x86_64.rpm-bundle.tar
    ```

- MySQL 압축 풀기 및 설치
  ```
  # tar -xzvf MySQL-5.1.73-1.glibc23.x86_64.rpm-bundle.tar
  # yum localinstall -y MySQL-server-5.1.73-1.glibc23.x86_64.rpm 
  # yum localinstall -y MySQL-client-5.1.73-1.glibc23.x86_64.rpm  
  # usr/bin/mysqladmin -u root password '...'
  # /usr/bin/mysql_secure_installation
  # mysql -u root -p
  ```
  - 설치시 오류 중 한 형태 : CentOS7에 mariaDB가 설치되어 충돌이 발생하기 때문에 mariaDB 삭제 후 설치
   ```
   # yum list installed mariadb\*
   # yum remove -y mariadb
   ```
  

# Installing SonarQube in CentOS/Redhat/Fedora

## Prerequisites

1. Java-1.8* or later
2. MySQL Database Server or MyQL RDS instance

Note:
Update: for some reasons java-1.8/java8 not works then install java 11/java-openjdk11
search in amazon-linux-extras by execting a command "amazon-linux-extras install java-openjdk11"

## Install MySQL client version

For CentOs:

```sh
yum install mysql
```

For Debian:

```sh
sudo apt install mysql-server
```

Secure

Download stable SonarQube version from official website.

Website: <https://www.sonarqube.org/downloads/>
Note: This Article written for SonarQube6.0

## Download & install SonarQube

```sh
cd /opt
apt install unzip
wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-8.9.7.52159.zip
unzip sonarqube-8.9.7.52159.zip
mv sonarqube-8.9.7.52159 sonar
```

## Create New User

SonarQube cannot run as root on Unix-based systems, so create a dedicated user accoun ftor SonarQube.

```sh
useradd sonar
passwd sonar
```

## Grant new user:sonar root access by editing /etc/sudoers file using visudo

```sh
sudo visudo
```

Add below commands at the end of sudoers file

```sh
sonar   ALL=(ALL:ALL) ALL
sonar   ALL=(ALL)   NOPASSWD: ALL
```

> root   ALL=(ALL:ALL) ALL

This means that our root user can run any command using sudo, as long as they provide their password.

1. The first field indicates the username that the rule will apply to (root).
2. The first “ALL” indicates that this rule applies to all hosts.
3. Second “ALL” indicates that the root user can run commands as all users
4. Third “ALL” indicates that the root user can run commands as all groups.
5. The last “ALL” indicates these rules apply to all commands

> sonar ALL=(ALL)  NOPASSWD: ALL

This means that our root user can run any command using sudo, without providing their password.

## Change owner permissions for sonar directory

```sh
cd /opt
chown -R sonar:sonar sonar
ls -lrth
```

Outputwould be like:

```sh
total 153M
drwxr-xr-x  2 root  root     6 Aug 16  2018 rh
drwxr-xr-x 11 sonar sonar  141 Nov 20  2018 sonar
-rw-r--r--  1 root  root  153M Nov 20  2018 sonarqube-6.7.6.zip
drwxr-xr-x  4 root  root    33 Apr 29 00:16 aws
```

## Allow RDS instance security group to access SonarQube server

Connect to RDS instance with database credentials

```sh
mysql -h <RDS_Instance_endpoint>:3306 -u <DB_USER_NAME> -p <DB_PASSWORD>
```

***Note:*** Sometimes port number and DB_PASSWORD may not required and can be used as below

WORKING TILL NOW

```sh
mysql -h <RDS_Instance_endpoint> -u <DB_USER_NAME> -p
```

## Create a new sonar database

```sh
CREATE DATABASE sonar CHARACTER SET utf8 COLLATE utf8_general_ci;
```

## Create a local and a remote user

```sh
CREATE USER sonar@localhost IDENTIFIED BY 'sonar';
CREATE USER sonar@'%' IDENTIFIED BY 'sonar';
```

## Grant database access permissions to users

```sh
GRANT ALL ON sonar.* TO sonar@localhost;
GRANT ALL ON sonar.* TO sonar@'%';
```

## Check users and databases

```sh
use mysql
show databases;
SELECT User FROM mysql.user;
FLUSH PRIVILEGES;
QUIT
```

### Edit sonar properties file to uncomment and provide required information for below properties

Edit the `sonar.properties` file

```sh
vi /opt/sonar/conf/sonar.properties
```

Find and edit below commands in the file

```sh
sonar.jdbc.username=sonar
sonar.jdbc.password=sonar
sonar.jdbc.url=jdbc:mysql://<RDS_DATABAE_ENDPOINT>:3306/sonar?useUnicode=true&characterEncoding=utf8&rewriteBatchedStatements=true&useConfigs=maxPerformance&useSSL=false
sonar.web.host=0.0.0.0
sonar.web.context=/
sonar.web.port=9000
```

## Start SonarQube service

```sh
sudo su - sonar
cd /opt/sonar/bin/linux-x86-64/
./sonar.sh start
```

> Run SonarQube as a default service

## Implement SonarQube server as a service

Copy `sonar.sh` to `etc/init.d/sonar` and modify it according to your platform.

```sh
sudo cp /opt/sonar/bin/linux-x86-64/sonar.sh /etc/init.d/sonar
sudo vi /etc/init.d/sonar
```

Add below values to your `/etc/init.d/` sonar file

```sh
vi /etc/init.d/sonar
```

Insert/modify below values into the sonar file

```sh
SONAR_HOME=/opt/sonar
PLATFORM=linux-x86-64

WRAPPER_CMD="${SONAR_HOME}/bin/${PLATFORM}/wrapper"
WRAPPER_CONF="${SONAR_HOME}/conf/wrapper.conf"
PIDDIR="/var/run"
```

## Start SonarQube server

```sh
service sonar start
```

SonarQube application uses port 9000. access SonarQube from browser

> <http://EC2_PUBLIC_IP:9000/>

Default Username: admin
Default Password: admin

## Troubleshooting

* Check whether you enabled port 9000 in EC2 instance security group
* Check whether you enabled EC2 instance IP range in RDS security group

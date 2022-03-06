# Sonarqube Setup

SonarQube is an open-source static testing analysis software, it is used by developers to manage source code quality and consistency.

## Prerequisites

1. Need an EC2 instance (min t2.small)
2. Install Java-11

 ```sh
 apt-get update
 apt  list | grep openjdk-11
 apt-get install openjdk-11-jdk -y
 ```

## Install & Setup Postgres Database for SonarQube

`Source: https://www.postgresql.org/download/linux/ubuntu/`  

1. Install Postgres database

   ```sh
   sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/ apt/sources.list.d/pgdg.list'
   wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
   sudo apt-get update
   sudo apt-get -y install postgresql
   ```

2. Set a password and connect to database (setting password as "admin" password)

   ```sh
   sudo passwd postgres
   su - postgres
   ```

3. Create a database user and database for sonarqube

   ```sh
   createuser sonar
   psql
   ALTER USER sonar WITH ENCRYPTED PASSWORD 'admin';
   CREATE DATABASE sonarqube OWNER sonar;
   GRANT ALL PRIVILEGES ON DATABASE sonarqube to sonar;
   ```

4. Restart postgres database to take latest changes effect

   ```sh
   systemctl restart postgresql 
   systemctl status postgresql
   ```

5. Check and verify that postgres is running on port `5432`

   ```sh
   apt install net-tools
   netstat -tulpn
   ```

   **Check point**: You should see postgres is running on `5432`

6. Add below entries in `/etc/sysctl.conf`

   ```sh
   vm.max_map_count=524288
   fs.file-max=131072
   ulimit -n 131072
   ulimit -u 8192
   ```

7. Add below entries in `/etc/security/limits.conf`

   ```sh
   sonarqube   -   nofile   131072
   sonarqube   -   nproc    8192
   ```

8. reboot the server

   ```sh
   init 6
   ```

==============================================================================================

## SonarQube Setup

1. Download [soarnqube](https://www.sonarqube.org/downloads/) and extract it.

   ```sh
   cd /opt
   wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-8.9.2.46101.zip
   unzip sonarqube-8.9.2.46101.zip
   ```

2. Update `sonar.properties` with below information `/opt/sonarqube/conf/sonar.properties`

   ```sh
   sonar.jdbc.username=<sonar_database_username>
   sonar.jdbc.password=<sonar_database_password>
   sonar.jdbc.url=jdbc:postgresql://<DB_ENDPOINT>:<PORT>/sonarqube?currentSchema=my_schema

   #Example:
   #sonar.jdbc.username=sonar
   #sonar.jdbc.password=admin
   #sonar.jdbc.url=jdbc:postgresql://localhost/sonarqube
   #sonar.search.javaOpts=-Xmx512m -Xms512m -XX:MaxDirectMemorySize=256m -XX:+HeapDumpOnOutOfMemoryError
   ```

3. Create a `/etc/systemd/system/sonarqube.service` file to start sonarqube service at the boot time

   ```sh
   cat >> /etc/systemd/system/sonarqube.service <<EOL
   [Unit]
   Description=SonarQube service
   After=syslog.target network.target

   [Service]
   Type=forking
   User=sonar
   Group=sonar
   PermissionsStartOnly=true
   ExecStart=/opt/sonarqube/bin/linux-x86-64/sonar.sh start 
   ExecStop=/opt/sonarqube/bin/linux-x86-64/sonar.sh stop
   StandardOutput=syslog
   LimitNOFILE=65536
   LimitNPROC=4096
   TimeoutStartSec=5
   Restart=always

   [Install]
   WantedBy=multi-user.target
   EOL
   ```

4. Add sonar user and grant ownership to `/opt/sonarqube` directory

   ```sh
   useradd -d /opt/sonarqube sonar
   cd /opt
   chown -R sonar:sonar sonarqube
   ls -lrth
   ```

5. Reload the demon and start sonarqube service

   ```sh
   systemctl daemon-reload 
   systemctl start sonarqube.service 
   ```

## Unable to access Sonarqube from browser?

 1. Make sure port 9000 is opened at security group
 2. Start sonar service as a sonar user
 3. User correct database credentials in the sonar.properties
 4. Use instance which has atleast 2 GB of RAM

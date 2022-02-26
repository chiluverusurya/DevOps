# SonarQube Issues that are resolved

## SonarQube starts and runs for a few seconds and then stops

One of the reason for this issue is because of misconfiguration of sonar.properties file in path `vi /opt/sonar/conf/sonar.properties`

you can resolve this issue by using correct configuration at this point mentioned below

> `sonar.jdbc.url=jdbc:mysql://<RDS_DATABAE_ENDPOINT>:3306/sonar?`

## Not able to connect to database server

If you are not able to connect to the external database then check for your database network ports in security groups

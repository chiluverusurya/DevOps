# Tomcat installation on Linux

## Prerequisites

1. EC2 instance
2. Java v1.8.x

## Install Apache Tomcat

Download tomcat packages from  <https://tomcat.apache.org/download-80.cgi> onto /opt on EC2 instance

## Create a tomcat directory

```sh
cd /opt
wget http://mirrors.fibergrid.in/apache/tomcat/tomcat-8/v8.5.35/bin/apache-tomcat-8.5.35.tar.gz
tar -xvzf /opt/apache-tomcat-8.5.35.tar.gz
```

## Rename the extracted directory to `tomcat`

```sh
mv apache-tomcat-8.5.35 tomcat
```

## Give executing permissions to startup.sh and shutdown.sh which are under bin

```sh
chmod +x /opt/tomcat
```

## Create soft link files for tomcat startup.sh and shutdown.sh

```sh
ln -s /opt/apache-tomcat-8.5.35/bin/startup.sh /usr/local/bin/tomcatup
ln -s /opt/apache-tomcat-8.5.35/bin/shutdown.sh /usr/local/bin/tomcatdown
tomcatup
```

### check point

Access tomcat application from browser on port 8080  

> <http://Public_IP:8080>

## Change the default port for tomcat

Using unique ports for each application is a best practice in an environment. But tomcat and Jenkins runs on ports number 8080. Hence lets change tomcat port number to your desired custom port. Change port number in `conf/server.xml` file under tomcat home
Update port number in the `connecter port` field in `server.xml`

```sh
vi /opt/apache-tomcat-8.5.35/conf/server.xml
```

## Restart tomcat after configuration update

```sh
tomcatdown
tomcatup
```

## Check Tomcat server status

Access tomcat application from browser on your custom port

> <http://Public_IP:8080>

Now application is accessible on custom port, but tomcat application doesn't allow to login from browser. Changing a default parameter in context.xml solves this issue

Search for context.xml file

```sh
find / -name context.xml
```

Above command gives 3 context.xml files. comment (<!-- & -->) `Value ClassName` field on files which are under webapp directory.
After that restart tomcat services to effect these changes

```sh
tomcatdown
tomcatup
```

Update users information in the `tomcat-users.xml` file
goto tomcat home directory and add below users to `conf/tomcat-user.xml` file

```sh
<role rolename="admin-gui"/>
<role rolename="manager-gui"/>
<role rolename="manager-script"/>
<role rolename="manager-jmx"/>
<role rolename="manager-status"/>
<user username="admin" password="admin" roles="admin-gui, manager-gui, manager-script, manager-jmx, manager-status"/>
<user username="deployer" password="deployer" roles="manager-script"/>
<user username="tomcat" password="s3cret" roles="manager-gui"/>
```

Restart serivce and try to login to tomcat application from the browser. This time it should be Successful

```sh
tomcatdown
tomcatup
```

# Install Maven

Apache Maven is a software project management and comprehension tool. Based on the concept of a project object model (POM), Maven can manage a project's build, reporting and documentation from a central piece of information.

## Prerequisites

1. Java-1.8*

## Install Maven on Jenkins or another server

Download maven packages from its official site `<https://maven.apache.org/download.cgi`
In this case I am using `/opt/maven` as my installation directory.

## Creating maven directory under /opt

```sh
mkdir /opt/maven
cd /opt/maven 
```

## Download and extract maven package

```sh
wget https://dlcdn.apache.org/maven/maven-3/3.8.4/binaries/apache-maven-3.8.4-bin.zip
unzip /opt/maven/apache-maven-3.8.4-bin.zip
```

or

```sh
wget https://dlcdn.apache.org/maven/maven-3/3.8.4/binaries/apache-maven-3.8.4-bin.tar.gz
tar -xzvf /opt/maven/apache-maven-3.8.4-bin.tar.gz
```

## Set Maven in environment variables path

Set `MAVEN_HOME` as environment variables on Jenkins machine where `JAVA_HOME` has been set while installing java.

Open the file profile to edit environment variables

```sh
vi /etc/profile
```

or

```sh
vi ~/.bash_profile
```

Edit the file with below statements at the end of the file

```sh
MAVEN_HOME="/opt/apache-maven-3.6.1"
JAVA_HOME="/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.201.b09-0.amzn2.x86_64"
PATH=$PATH:$JAVA_HOME:$JAVA_HOME/bin:$MAVEN_HOME/bin
```

***Note: Provide the correct Maven installation path***

### Reload the configuration file

```sh
source /etc/profile
```

or

```sh
source ~/.bash_profile
```

## Check the installed maven version

```sh
mvn –version
```

So far you have completed installation of maven software to support maven plugin on jenkins console. Let's jump onto jenkins to complete remaining steps.

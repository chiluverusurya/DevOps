# Installing Java in CentOs/Debian

To check whether java is installed or not execute the below command.

```sh
java -version
```

## Install Java

We will be using open java for our demo, Get the latest version from <http://openjdk.java.net/install/>

Perform the installation as a "root" user.

```sh
sudo su -
```

**Choose below command with respect to your OS:**

***CentOs:***

```sh
yum install -y java-1.8*
```

***Debian:***

```sh
apt-get install -y openjdk-8-jdk
```

## Check for installed java version

```sh
java -version
```

## Check java installation path

```sh
which java
```

Output would be like `/usr/bin/java` (This is default installation path of java)

## Set Java to enviroment variables path

Check the path of your java installation

```sh
find /usr/lib/jvm/java-1.8* | head -n 3
```

Output would be like:

```text
/usr/lib/jvm/java-1.8.0
/usr/lib/jvm/java-1.8.0-openjdk
/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.282.b08-1.amzn2.0.1.x86_64
```

Copy the java path in 3rd line of output

## Set "JAVA_HOME" as environment variable in "/etc/profile" or "~/.bash_profile"

```sh
vi /etc/profile
```

or

```sh
vi ~/.bash_profile
```

Add below statements at the end of "profile" file

```sh
JAVA_HOME="/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.201.b09-0.amzn2.x86_64"
PATH=$PATH:$HOME/bin:$JAVA_HOME:$JAVA_HOME/bin
```

save & close the file (by using :wq!)
> ***Note:*** provide your correct Java installation path

## Reload the configuration file

```sh
source /etc/profile
```

or

```sh
source ~/.bash_profile
```

## Now check the path

```sh
which java
```

Or you can also check in the environment variables path

```sh
echo $PATH
```

Output should be like:

> /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.282.b08-1.amzn2.0.1.x86_64/bin/java

Now, Java path has been succesfully installed and set in environment variables.

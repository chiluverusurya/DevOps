# Install Jenkins on AWS EC2

Jenkins is a self-contained Java-based program, ready to run out-of-the-box, with packages for Windows, Mac OS X and other Unix-like operating systems. As an extensible automation server, Jenkins can be used as a simple CI server or turned into the continuous delivery hub for any project.

## Prerequisites

1. EC2 Instance
2. Java v1.8.x or higher
3. Security Group with Port 8080 open for internet
4. With Internet Access

## Installing Jenkins

You can install jenkins using the rpm or by setting up the repo. We will set up the repo so that we can update it easily in the future.

Get the latest version of jenkins from jenkin's official website <https://pkg.jenkins.io/redhat-stable/>

**Use below command with respect to your os:**

***Centos:***

```sh
sudo yum -y install wget
```

***Debian:***

```sh
sudo apt-get -y install wget
```

## Download jenkins packages to install

***CentOs:***

```sh
sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key  
```

***Debian:***

```sh
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo tee /usr/share/keyrings/jenkins-keyring.asc > /dev/null
```

Then add a Jenkins apt repository entry:

```sh
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
```

## Enter the below command to install jenkins

**Use below command with respect to your os:**

***Centos:***

```sh
sudo apt-get update
sudo yum install jenkins
```

***Debian:***

```sh
sudo apt-get update
sudo apt-get -y install jenkins
```

## Start Jenkins

***Centos/Debian:***

```sh
service jenkins start
```

or

```sh
systemctl start jenkins
```

## Setup Jenkins to start at boot

```sh
systemctl enable jenkins
```

or

```sh
chkconfig jenkins on
```

## Accessing Jenkins

By default jenkins runs at port 8080, You can access jenkins at

> <http://YOUR_SERVER_PUBLIC_IP:8080>

In case you want to change the default jenkins port on Linux, you can go to `/etc/sysconfig/jenkins` and change `JENKINS_PORT="8080"` to `JENKINS_PORT="<YOUR_PORT_NO>"`

Then you should restart Jenkins service.

```sh
sudo service jenkins restart
```

## Configure Jenkins

* To get started with jenkins copy the secret text location shown on jenkins user interface.

  Grab the default password from Password Location:/var/lib/jenkins/secrets/initialAdminPassword

  ```sh
  cat /var/lib/jenkins/secrets/initialAdminPassword
  ```

* Copy the secret text and paste it on jenkins page to start using jenkins.

* On the next page select standard plugin installation and skip custom Plugin Installation for now to install necessary plugins later.

* Next on the Getting Started page - Create First Admin User
  * Username
  * Password
  * Confirm Password
  * Full Name
  * E-mail address

## Configure java path in Jenkins

> Manage Jenkins > Global Tool Configuration > JDK

## Test Jenkins Jobs

1. Create “new item”
2. Enter an item name => My-First-Project
3. Choose Freestyle project
4. Under Build section Execute shell : `echo "Welcome to Jenkins Demo"`
5. Save your job
6. Build job
7. Check "console output"

> After running your first job a workspace folder will be created by jenkins to store your jobs data at `/var/lib/jenkins/workspace`

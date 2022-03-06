# Installing Jfrog Artifactory

Jfrog artifactory is written in java and it is a webapp runs on tomcat and it is available as opensource and also as pro version which requires a paid license for additional benifits.

## Pre-requisites

* Java-1.8*

## Installation steps

1. Switch to root user

   ```sh
   sudo su -
   ```

2. Download and extract Artifaction packages from official website in directory "/opt"

   ```sh
   cd /opt
   wget https://releases.jfrog.io/artifactory/bintray-artifactory/org/artifactory/oss/   jfrog-artifactory-oss/[RELEASE]/jfrog-artifactory-oss-[RELEASE]-linux.tar.gz
   uzip jfrog-artifactory-oss-\[RELEASE\]-linux.tar.gz
   tar -zxvf jfrog-artifactory-oss-\[RELEASE\]-linux.tar.gz
   ```

3. Rename the directory to jfrog (Optional)

   ```sh
   mv artifactory-oss-7.19.8/ jfrog
   ```

4. Start artifactory services from bin directory in downloaded package

   ``` sh
   cd jfrog/app/bin
   ./artifactory.sh start
   ```

5. Access artifactory from browser
   By default Jfrog Artifactory runs at the port 8081 and redirects to 8082. So, you must open these ports in security group to access jfrog artifactory from browser.

   * Default port: 8081 (Redirects to 8082)
   * Default username: admin
   * Default password: password

## Integratring Jfrog with Jenkins

### Intall Jenkins plugin for Jfrog Artifactory

Manage Jenkins -> Manage Plugins -> Search for "Artifactory Plugin" -> Install without restart

### Configure Jenkins

Manage Jenkins -> Configure System -> Artifactory

* Server Id: artifactory
* Url: <repo_url>:8081/artifactory
* Default Deployer Credentials: Create a new user for this (Optional)
  * username: admin or jenkinsuser
  * password: <repo_password>

In freestyle pipeline update pom.xml with artifactory info (Distribution Management code) auto-generated via setupme

If Required: Update settings.xml in maven directory for credentials of artifactory server

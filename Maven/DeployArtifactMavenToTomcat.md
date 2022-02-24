# Deploy Artifact From Maven to Tomcat

If we want to use Maven for deploying our web archives, first we must need to edit two files.

1. Edit settings.xml for credentials

   There are two locations where the settings.xml file may be found:

   - The Maven install: ${maven.home}/conf/settings.xml
   - A user’s install: ${user.home}/.m2/settings.xml

   Once we have found it, we'll configure Tomcat server credentials:

   ```sh
   <server>
       <id>TomcatServer</id>
       <username>admin</username>
       <password>password</password>
   </server>
   ```

   Now we'll need a basic web application from Maven to test the deployment.
   Let's navigate to where we would like to create the application.

   Download archetype maven-archetype-webapp

   We'll run this command on the console to create a new Java web application using maven archetype.

   ```sh
   mvn archetype:generate -DgroupId=com.baeldung -DartifactId=tomcat-war-deployment 
     -DarchetypeArtifactId=maven-archetype-webapp -DinteractiveMode=false
   ```

   This will create a complete demo web application in the current directory, which will print hello world! if    we deploy it now and access it via the browser.

   But before we do that, we need to make one more change to enable Maven deployment.
   Let's head over to the pom.xml in current webapp project and add this plugin.

2. Edit pom.xml code to add maven plugin to copy artifacts onto tomcat, this should be under `build`

   ```sh
   <plugin>
       <groupId>org.apache.tomcat.maven</groupId>
       <artifactId>tomcat7-maven-plugin</artifactId>
       <version>2.2</version>
       <configuration>
           <url>http://localhost:8080/manager/text</url>
           <server>TomcatServer</server>
           <path>/myapp</path>
       </configuration>
   </plugin>
   ```

   Note that we're using the Tomcat 7 plugin because it works for both versions 7 and 8 without any special    changes.

   The configuration url is the url to which we're sending our deployment, and Tomcat will know what to do with    it.
   The server element is the name of the server instance that Maven recognizes. Finally, the path element    defines the context path of our deployment.

   This means that if our deployment succeeds, we'll access the web application by hitting <http://   localhost:8080/myapp>

   Now we can run the following commands from Maven.

## To deploy the web app

```sh
mvn tomcat7:deploy
```

## Then to undeploy it

```sh
mvn tomcat7:undeploy
```

## Finally, to redeploy it after making changes

```sh
mvn tomcat7:redeploy
```

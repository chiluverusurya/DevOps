# Plugins for Jenkins

## Ansible Plugins to install in jenkins

### Publish over SSH plugin

> `Publish over SSH`

Install "Maven Integration" Plugin without restart

- `Manage Jenkins` > `Jenkins Plugins` > `available` > `Publish over SSH`

To install/deploy artifacts using jenkins via ansible install a plugin `publish over ssh`, this plugin sends build artifacts to deploy

## Install required maven plugins for jenkins

### Maven Integration

> `Maven Integration`

Install "Maven Integration" Plugin without restart

- `Manage Jenkins` > `Jenkins Plugins` > `available` > `Maven Integration`

### Maven Invoker

> `Maven Invoker`

Install "Maven Invoker" plugin without restart

- `Manage Jenkins` > `Jenkins Plugins` > `available` > `Maven Invoker`
  
### Configure maven path in jenkins

- `Manage Jenkins` > `Global Tool Configuration` > `Maven`

## Plugins for deploying to tomcat server

### Deploy to container

Add the `Deploy WAR/EAR to a container` Jenkins plugin

Out of the box, there are no built-in features that perform a Jenkins WAR file deployment to Tomcat.

That means a Jenkins Tomcat deploy plugin must be installed in the CI tool to make a deployment happen.

> `Deploy to container`

Install "Deploy to container" plugin without restart

- `Manage Jenkins` > `Jenkins Plugins` > `available` > `Deploy to container`

The most popular Jenkins Tomcat deployment plugin is named `Deploy to container`, which can be installed through the Plugin Manager tab under the `Manage Jenkins` section of the tool.

## jenkins job dsl plugin

### Job DSL

> `Job DSL`

Install "Job DSL" plugin without restart

- `Manage Jenkins` > `Jenkins Plugins` > `available` > `Job DSL`

You can view its related documentation here: <https://jenkinsci.github.io/job-dsl-plugin/>

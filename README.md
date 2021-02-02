[![Gitter](https://badges.gitter.im/quartz-manager/community.svg)](https://gitter.im/quartz-manager/community?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge)

# QUARTZ MANAGER
UI Manager for Quartz Scheduler.

Through this webapp you can launch and control your scheduled job. The UI Console is composed by a management panel to set trigger, start/stop scheduler and a log panel with a progress bar to display the job output. 

![](https://github.com/fabioformosa/quartz-manager/blob/master/quartz-manager-api/src/main/resources/quartz-manager-2-screenshot_800.PNG)

## HOW IT WORKS
* Set up the trigger into the left sidebar in terms of: daily frequency and and max occurrences.
* Press the start button
* The GUI manager updates the progress bar and reports all logs of your quartz job.

## ROADMAP
Open the [Project Roadmap](https://github.com/fabioformosa/quartz-manager/projects) to take a look at the plan of Quartz Manager.  
Currently this project might be useful to look how to import Quartz Library in a spring boot application. For this purpose, browse the folder `quartz-manager-parent/quartz-manager-api`.  
We're just working to create a library, from project `quartz-manager-parent/quartz-manager-api`, to be imported in your spring boot where you have your job to be scheduled.  
The project [Quartz-Manager Demo](https://github.com/fabioformosa/quartz-manager-demo) is an example of how-to:
 * import the quartz-manager-api library
 * include the quartz-manager frontend (angular based) through a webjar
 * set the application.yml
 * add secure layer to allow the API only to logged users
 * schedule a custom job (a dummy `hello world`)
 
 **NB**: In few days, we'll release the library jar of quartz-manager into the maven central repo.

Next steps in the roadmap are:
* to add a persistent layer to save all job setup.
* to add a complete setup UI panel for quartz, in term of cronjobs and multiple jobs.
* to add CI/CD pipeline to ease the deploy pulling a docker container.
* Enabling adapters for integrations: kafka, etc.

## PROJECT STRUCTURE
* **quartz-parent/quartz-manager-api** is the library that can be imported in webapp to have the quartz-manager API.
* **quartz-parent/quartz-manager-webjar** is a maven module to build and package the angular frontend in a webjar.
* **quartz-parent/quartz-manager-security** is ther library that can be imported in a webapp to have a security layer (login) over the quartz-manager API.
* **quartz-parent/quartz-manager-web-showcase** is an example of webapp that imports quartz-manager-api. Useful to develop the frontend started locally with the webpack dev server.
* **quartz-frontend** is the angular app that interacts with the Quartz Manager API.

## HOW-TO CONTRIBUTE
**[requirements]** Make sure you have installed
* [Java 8](https://java.com/download/) or greater
* [Maven](https://maven.apache.org/)
* [npm](https://www.npmjs.com/get-npm), [node](https://nodejs.org) and [angular-cli](https://cli.angular.io/)

To build&run quartz-manager in your machine:

```
#CLONE REPOSITORY
git clone https://github.com/fabioformosa/quartz-manager.git

# START QUARTZ-MANAGER-WEB
cd quartz-manager/quartz-parent/quartz-manager-web
mvn spring-boot:run

# START QUARTZ-MANAGER-FRONTEND
cd quartz-manager/quartz-manager-frontend
npm install
npm start

```

1. Open browser at [http://localhost:4200](http://localhost:4200)
1. Log in with **default credentials**: `admin/admin`

If you are not confident with maven CLI, you can start it by your IDE. For more details [spring boot ref.](http://docs.spring.io/spring-boot/docs/current/reference/html/using-boot-running-your-application.html)


## HOW TO RUN YOUR SCHEDULED JOB
By default, quartz-manager-web executes the dummy job that logs "hello world!".
Replace the dummy job (class: `it.fabioformosa.quartzmanager.jobs.SampleJob`) with yours. Follow these steps:

1. Extend the super class `it.fabioformosa.quartzmanager.jobs.AbstractLoggingJob`
1. set property `quartz-manager.jobClass` with qualified name of your custom Job Class (default job is SampleJob.class)

## HOW TO CHANGE SETTINGS
* Num of Threads: `/quartz-manager-parent/quartz-manager-web/src/main/resources/quartz.properties`
* Credentials: To change admin's password, set ENV var `quartz-manager.account.pwd`
* quartz-manager backend context path (default `/quartz-manager`) and port (default `8080`): `/quartz-manager/src/main/resources/application.properties`

## HOW TO BROWSE REST API DOC
Swagger has been added as library. So, you can get REST API doc opening: [http://localhost:8080/quartz-manager/swagger-ui.html](http://localhost:8080/quartz-manager/swagger-ui.html)

## Tech Overview

**Backend Stack** Java 8, Spring Boot 2.1.4 (Spring MVC 5.1.6, Spring Security 5.1.5, Spring AOP 5.1.6), Quartz Scheduler 2.3.1

**Application Server** Tomcat (embedded)

**Frontend** Angular 9.1.4, Web-Socket (stompjs 2.3.3)

**Style** angular material, FontAwesome 5

From quartz manager ver 2.x.x, the new structure of project is:
 * REST API backend
 * Single Page Application frontend (angular 9)

(The previous version of quartz manager was a monolithic backend that provided also frontend developed with angularjs 1.6.x. You can find it at the branch 1.x.x)

## Contributes

Every contribution is welcome. Open a issue, so we can discuss about new features and implement them. 

## Credits

* this project has been created from [angular-spring-starter](https://github.com/bfwg/angular-spring-starter)



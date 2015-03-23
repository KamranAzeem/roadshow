# Calculator web app demo project

Calculator web application demo project, used for various 
training classes around continuous delivery by Praqma.

The project was earlier called [Praqma training RoadShow](https://github.com/praqma-training/roadshow), so there is a bit legacy and some hack, leaving room for exercises :-)


## Short summary

* Uses Gradle to build
* Can deploy web app t Tomcat server
* Can run Selenium tests againt deployed web app
* Release and publishing of artifacts are supported

* You only need a JVM to run Gradle for playing with the basic setup on your own machine.

## Gradle as build tool

The project uses Gradle as build tool, and as such only requires you have JVM to run gradle.

To use gradle in the project, run the gradle wrapper script (which is checked into the repository):

* Linux: `./gradlew` (_this will be used in examples below_)
* Windows: `./gradlew.bat`

It will list a short help.

Gradle uses the concept of a _task_ for what to do, like build, run tests etc.

The _Gradle wrapper script_ (`gradlew` and `gradlew.bat`) is part of the project to ensure only a JVM is needed as dependency for building. Gradle will take care of the rest.


## Build howto

This could some of the things you would like to do in your Jenkins jobs.

### Build and test

Build source, compile unit test and run unit test:

`./gradlew war test`

Build _war_ file that can be deployed to Tomcat, and reports unit test results to `build/test-results/`.

To enable manual build support on a Jenkins job, use the special `jenkinstest` task instead of `test` to ensure new timestamps on junit outpu files that the Jenkins JUnit plugin requires.

`./gradlew war jenkinstest`

### Cleaning

Cleaning, doing every gradle tasks from scratch:

`./gradlew clean`


### Coverage of unit test

`./gradlew jacocoTestReport` tasks measures and reports coverage on unit tests.


### Static analysis

You can run all supported static analysis checks with:

`./gradlew staticanalysis`

It will check on both main and test sources and report to xml files.

There are different analysis available:

* PMD
* checkstyle
* Fingbugs
* jdepend

They all have both a _Main_ and _Test_ task, that analysis respectively main sources or test sources.
For example `pmdMain` or `findbugsTest`.

### Checking

The built in gradle tasks `check` will also run all of the static analysis tools goals, including the `test` tasks which is unit test.

`./gradlew check`


### Code documentation

You can generate javadoc on the sources with:

`./gradlew javadoc`




## Customize the project

For training classes, that uses shared artifact- and web-server, you need to make sure both webapp and artifact have a unique name.

Patch the following line in `build.gradle` replacing _mytrainingusername_ with your own name, initial or Github account id.

        ext.trainingUserName = 'mytrainingusername' // it is a good idea to chose the same as your github id


Test line by Kamran
Another line.

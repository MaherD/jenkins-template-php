jenkins-template-php
====================
The goal of this project is to provide a standard template for Jenkins jobs for PHP projects.

Required Jenkins Plugins

You need to install the following plugins for Jenkins:

    Checkstyle (for processing PHP_CodeSniffer logfiles in Checkstyle format)

    Clover PHP (for processing PHPUnit code coverage xml output)

    DRY (for processing phpcpd logfiles in PMD-CPD format)

    HTML Publisher (for publishing the PHPUnit code coverage report, for instance)

    JDepend (for processing PHP_Depend logfiles in JDepend format)

    Plot (for processing phploc CSV output)

    PMD (for processing PHPMD logfiles in PMD format)

    Violations (for processing various logfiles)

    xUnit (for processing PHPUnit logfiles in JUnit format)

You can install these plugins using the web frontend at

    http://localhost:8080/pluginManager/available

or using the Jenkins CLI:

    wget http://localhost:8080/jnlpJars/jenkins-cli.jar
    java -jar jenkins-cli.jar -s http://localhost:8080 install-plugin \
    checkstyle cloverphp dry htmlpublisher jdepend plot pmd violations xunit

    java -jar jenkins-cli.jar -s http://localhost:8080 safe-restart

In the above, replace localhost:8080 with the hostname and port of your Jenkins installation.

Here is an overview of the tasks defined in the above build.xml (download) script that are intended to be directly invoked:

    build is the default build target. It invokes all the tools in such a way that XML logfiles are written to default locations.

    build-parallel is the same as build (see above) except that it executes the tools in parallel.

    clean can be used to clean up (delete) all build artifacts (logfiles, etc. that are produced during the build).

    lint can be used to perform a syntax check of the project sources using php -l.

    phpdox can be used to generate API documentation.

    phpcs can be used to find coding standard violations and print human readable output. This task is intended for usage on the command line before committing.

    phploc can be used to measure the project size.

    phpmd can be used to perform project mess detection and print human readable output. This task is intended for usage on the command line before committing.

    phpunit can be used to run unit tests.

The other tasks can, of course, also be invoked directly but that is not their intended purpose. They are invoked by the tasks listed above.

Using the Job Template

1- Fetch the jenkins-cli.jar from your jenkins server:

    wget http://localhost:8080/jnlpJars/jenkins-cli.jar

2- Download and install the job template:

    curl https://github.com/MaherD/jenkins-template-php/master/config.xml | \
        java -jar jenkins-cli.jar -s http://localhost:8080/jenkins create-job php-template

or add the template manually:

    cd $JENKINS_HOME/jobs
    mkdir php-template
    cd php-template
    wget https://github.com/MaherD/jenkins-template-php/master/config.xml
    cd ..
    chown -R jenkins:jenkins php-template/

3- Reload Jenkins' configuration, for instance using the Jenkins CLI:

    java -jar jenkins-cli.jar -s http://localhost:8080 reload-configuration

4- Click on "New Job".

5- Enter a "Job name".

6- Select "Copy existing job" and enter "php-template" into the "Copy from" field.

7- Click "OK".

8- Disable the "Disable Build" option.

9- Fill in your "Source Code Management" information.

10- Configure a "Build Trigger", for instance "Poll SCM".

11- Click "Save".



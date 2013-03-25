jenkins-template-php
====================

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


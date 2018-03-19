Docker Images
=============

<a href="https://raw.githubusercontent.com/KoskiLabs/docker-images/master/LICENSE">
    <img src="https://img.shields.io/hexpm/l/plug.svg"
         alt="License: Apache 2">
</a>
<a href="https://travis-ci.org/KoskiLabs/docker-images/">
    <img src="https://travis-ci.org/KoskiLabs/docker-images.png"
         alt="Travis Build">
</a>
<a href="https://github.com/KoskiLabs/builder/releases">
    <img src="https://img.shields.io/github/release/KoskiLabs/builder.svg"
         alt="Releases">
</a>

Docker image definitions for Koski Labs projects managed as [Maven](https://maven.apache.org/) sub-modules, built and published to Docker Hub using [Fabric 8's Maven Docker plugin](https://dmp.fabric8.io/).

Quick Start
-----------

<>

Usage
-----

<>

Prerequisites
-------------

Only requires [Docker](https://www.docker.com/community-edition) daemon to be installed and running.

Building
--------

To build all docker images:

    docker-images> ./jdk-wrapper.sh ./mvnw verify

However, you can also build only a specific sub-module (docker image) by invoking:

    docker-images> echo "Module:"; read MODULE; ./jdk-wrapper.sh ./mvnw -pl ${MODULE} verify

All builds must be executed from the root of the project.

Releasing
---------

Sub-modules in this project are versioned and released independently. Releases are performed using the [Maven release plugin](https://maven.apache.org/maven-release/maven-release-plugin/index.html)
which updates the sub-module version and SCM tag in the sub-module's _pom.xml_ based on your input. The plugin performs two updates as
separate commits; first, to commit the next release version, and second to commit the next developer version. Travis will builds each of
these commits publishing artifacts (in this case Docker images) to the configured release repositories (in this case [Docker Hub](https://hub.docker.com/u/koskilabs/)).

Before releasing a new version of a subm-module, determine the appropriate version change (X, Y or Z) based on the change history since the
most recent release (don't forget to rebase!). Please see [semver.org](http://semver.org/) for more information on how to version artifacts.
Next, simply invoke the Maven Release plugin which will ask for the sub-module name, release version and the next development version.

    docker-images> echo "Module:"; read MODULE; ./jdk-wrapper.sh ./mvnw -pl ${MODULE} release:prepare && ./jdk-wrapper.sh ./mvnw -pl ${MODULE} release:clean && git pull

License
-------

Published under Apache Software License 2.0, see LICENSE

&copy; Ville Koskela, 2018

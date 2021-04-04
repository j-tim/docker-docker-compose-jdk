# Jtim custom Gitlab CI build image with Docker, Docker-compose and (Adopt) OpenJDK 

Docker image that can be used in Gitlab CI build pipelines and run as non root!
We have support for both:
 
* Java 11 (AdoptOpenJdk)
  * Hotspot
  * OpenJ9
* Java 8 (Open JDK)

## Java 11 (latest) version images contains

* Docker version: 20.10.5, build 55c4c88
* Docker compose: 1.28.6
* Adopt Open JDK: 11.0.9+11 (Hotspot or Open9J)
* Git: 2.25.1
* Jq: 1.6
* Pack: 0.18.0+git-e00ee4a.build-2328

## Java 8 version images contains 

* Docker version: 20.10.2 ce
* Docker compose: 1.28.0
* Open JDK: 8u252
* Git: 2.26.2
* Jq: jq-master-v20200428-28-g864c859e9d
* Pack: 0.16.0+git-e0f6c50.build-1898

## Notes

### Running as non root

* Since version `18.09.3-ce-git-compose-1.23.2-adoptopenjdk-11.0.2.9` we added support for Java 11 (based on Adopt Open JDK ubuntu image) 
* Since version `18.05.0-ce-git-compose-1.21.2-openjdk-8u171` this image is not running as root anymore!

### Deprecated versions

Unfortunately Alpine Linux does not keep old packages.
So we consider our images deprecated when the openjdk apk packages are not available in for Alpine anymore. 

## Supported tags and respective Dockerfile links

### Supported versions

#### Java 11

**Hotspot**

* `20.10.5-compose-1.28.6-adoptopenjdk-11.0.10_9`, `adoptopenjdk-11.0.10_9`, `adoptopenjdk-11`, `11.0.10_9` [(latest)](https://github.com/j-tim/docker-docker-compose-jdk/blob/master/java11/adoptopenjdk/11.0.10_9/hotspot/Dockerfile)

* `18.09.6-ce-git-compose-1.24.0-adoptopenjdk-11.0.3_7`, `adoptopenjdk-11.0.3_7`, `adoptopenjdk-11`, [(11.0.3.7)](https://github.com/j-tim/docker-docker-compose-jdk/blob/master/java11/adoptopenjdk/11.0.3_7/hotspot/Dockerfile)

* `18.09.3-ce-git-compose-1.23.2-adoptopenjdk-11.0.2.9`, `adoptopenjdk-11.0.2.9`, [(11.0.2.9)](https://github.com/j-tim/docker-docker-compose-jdk/blob/master/java11/adoptopenjdk/11.0.2.9/hotspot/Dockerfile)

**OpenJ9**

* `20.10.5-compose-1.28.6-adoptopenjdk-11.0.9.1_1_openj9-0.23.0`, `adoptopenjdk-11.0.9.1_1_openj9-0.23.0`, `adoptopenjdk-11-openj9`, [(11.0.9.1_1_openj9-0.23.0)](https://github.com/j-tim/docker-docker-compose-jdk/blob/master/java11/adoptopenjdk/11.0.10_9/openJ9/Dockerfile)


* `18.09.6-ce-git-compose-1.24.0-adoptopenjdk-11.0.3_7_openj9-0.14.3`, `adoptopenjdk-11.0.3_7-openj9`,  [(adoptopenjdk-11-openj9)](https://github.com/j-tim/docker-docker-compose-jdk/blob/master/java11/adoptopenjdk/11.0.3_7/openJ9/0.14.3/Dockerfile)

#### Java 8

* `20.10.2-ce-git-compose-1.28.0-openjdk-8u252`, `20.10.2-compose-1.28.0-openjdk-8u252` `openjdk-8u252`, `openjdk-8`, [(8u252)](https://github.com/j-tim/docker-docker-compose-jdk/blob/master/java8/openjdk/8u252/Dockerfile)

### Deprecated images 

* `18.09.1-ce-git-compose-1.23.1-openjdk-8u201`, `openjdk-8u201`, `openjdk-8`, [(8u201)](https://github.com/j-tim/docker-docker-compose-jdk/blob/master/java8/openjdk/8u201/Dockerfile)
* `18.09.1-ce-git-compose-1.23.1-openjdk-8u191`, `openjdk-8u191`, [(8u191)](https://github.com/j-tim/docker-docker-compose-jdk/blob/master/java8/openjdk/deprecated/8u191/Dockerfile)
* `18.05.0-ce-git-compose-1.21.2-openjdk-8u171`, `openjdk-8u171`,  [(8u171)](https://github.com/j-tim/docker-docker-compose-jdk/blob/master/java8/openjdk/deprecated/8u171/Dockerfile)
* `18.01.0-compose-1.18.0-openjdk-8u151`, `openjdk-8u151`, [(8u151)](https://github.com/j-tim/docker-docker-compose-jdk/blob/master/java8/openjdk/deprecated/8u151/Dockerfile)  
* `17.07-compose-1.16.1-openjdk-8u131`, `openjdk-8u131`, `8u131` [(8u131)](https://github.com/j-tim/docker-docker-compose-jdk/blob/master/java8/openjdk/deprecated/8u131/Dockerfile)  
* `17.04-compose-1.12.0-openjdk-8u121`, `openjdk-8u121`, [(8u121)](https://github.com/j-tim/docker-docker-compose-jdk/blob/master/java8/openjdk/deprecated/8u121/Dockerfile)  

## Pull the image 

```shell
docker pull jtim/docker-docker-compose-jdk
```

## How to use the Gitlab Build image

.gitlab-ci.yml

```
stages:
  - java

java-docker-job:
  image: jtim/docker-docker-compose-jdk:18.09.3-ce-git-compose-1.23.2-adoptopenjdk-11.0.2.9
  stage: java
  script:
    - whoami
    - docker -v
    - docker-compose -v
    - echo $CI_JOB_TOKEN | docker login -u gitlab-ci-token --password-stdin registry.gitlab.com
    - echo $DOCKER_HOST
    - java -version
    - git version
    - jq --version
    - pack --version
```

You don't need to set these variables in your pipeline we already set them in the Docker images:

```yml
variables:
  DOCKER_HOST: tcp://docker:2375
  DOCKER_DRIVER: overlay2
  DOCKER_TLS_CERTDIR: ""
```

## Related images

In case you just need Docker and Docker compose (non root) see: 

[https://hub.docker.com/r/jtim/docker-docker-compose](https://hub.docker.com/r/jtim/docker-docker-compose)
# Jtim custom Gitlab CI build image with Docker, Docker-compose and (Adopt) OpenJDK 

Docker image that can be used in Gitlab CI build pipelines and run as non root!
We have support for both:
 
* Java 8 (Open JDK) 
* Java 11 (Adopt Openjdk)

## Java 8 version images contains 

* Docker version: 18.09.1 ce
* Docker compose: 1.23.1
* Open JDK: 8u191
* Git: 2.18.1

## Java 11 (latest) version images contains 

* Docker version: 18.09.3 ce
* Docker compose: 1.23.2
* Adopt Open JDK: 11.0.2.9
* Git: 2.17.1

## Notes

* Since version `18.09.3-ce-git-compose-1.23.2-adoptopenjdk-11.0.2.9` we added support for Java 11 (based on Adopt Open JDK ubuntu image) 
* Since version `18.05.0-ce-git-compose-1.21.2-openjdk-8u171` this image is not running as root anymore!

## Supported tags and respective Dockerfile links

### Supported versions

#### Java 11

* `18.09.3-ce-git-compose-1.23.2-adoptopenjdk-11.0.2.9`, `adoptopenjdk-11.0.2.9`, `adoptopenjdk-11`, `11.0.2.9` [(latest)](https://github.com/j-tim/docker-docker-compose-jdk/blob/master/11.0.2.9/adoptopenjdk/Dockerfile)

#### Java 8

* `18.09.1-ce-git-compose-1.23.1-openjdk-8u191`, `openjdk-8u191`, `openjdk-8`, [(8u191)](https://github.com/j-tim/docker-docker-compose-jdk/blob/master/8u191/Dockerfile)

* `18.05.0-ce-git-compose-1.21.2-openjdk-8u171`, `openjdk-8u171`,  [(8u171)](https://github.com/j-tim/docker-docker-compose-jdk/blob/master/8u171/Dockerfile)

### Deprecated images 

* `18.01.0-compose-1.18.0-openjdk-8u151`, `openjdk-8u151`, [(8u151)](https://github.com/j-tim/docker-docker-compose-jdk/blob/master/8u151/Dockerfile)  
* `17.07-compose-1.16.1-openjdk-8u131`, `openjdk-8u131`, `8u131` [(8u131)](https://github.com/j-tim/docker-docker-compose-jdk/blob/master/8u131/Dockerfile)  
* `17.04-compose-1.12.0-openjdk-8u121`, `openjdk-8u121`, [(8u121)](https://github.com/j-tim/docker-docker-compose-jdk/blob/master/8u121/Dockerfile)  

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
    - java -version
    - git version
```

## Related images

In case you just need Docker and Docker compose (non root) see: 

[https://hub.docker.com/r/jtim/docker-docker-compose](https://hub.docker.com/r/jtim/docker-docker-compose)
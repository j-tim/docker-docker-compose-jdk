# Jtim custom Gitlab CI build image with Docker, Docker-compose and OpenJDK 8u171

## Supported tags and respective Dockerfile links

### Latest version

* Docker version: 18.05.0 ce-git
* Docker compose: 1.18.0
* Open JDK: 8u171

Since version `18.05.0-ce-git-compose-1.21.2-openjdk-8u171` this image is not running as root anymore!

* `18.05.0-ce-git-compose-1.21.2-openjdk-8u171`, `openjdk-8u171`, `openjdk-8`, `8u171` [(latest)](https://github.com/j-tim/docker-docker-compose-jdk/blob/master/8u171/Dockerfile)

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
  image: jtim/docker-docker-compose-jdk:18.05.0-ce-git-compose-1.21.2-openjdk-8u171
  stage: java
  script:
    - whoami
    - docker -v
    - docker-compose -v
    - java -version
```

## Related images

In case you just need Docker and Docker compose see: 

[https://hub.docker.com/r/jtim/docker-docker-compose](https://hub.docker.com/r/jtim/docker-docker-compose)
FROM adoptopenjdk/openjdk11:jdk-11.0.3_7

# Default to UTF-8 file.encoding
ENV LANG C.UTF-8

ENV DOCKER_HOST tcp://docker:2375/

# Setup the non root user and group
ENV NON_ROOT_CONTAINER_USER bob-the-builder
ENV DOCKER_COMPOSE_VERSION 1.24.0
ENV DOCKER_COMPOSE_BASE_DOWNLOAD_URL https://github.com/docker/compose/releases/download

RUN groupadd ${NON_ROOT_CONTAINER_USER} \
    && useradd -rm -d /home/${NON_ROOT_CONTAINER_USER} -s /bin/bash -g 1000 -G ${NON_ROOT_CONTAINER_USER} -u 1000 ${NON_ROOT_CONTAINER_USER}

RUN apt update \
    && apt install -y apt-transport-https ca-certificates curl gnupg-agent software-properties-common \
    && curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add - \
    && add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" \
    && apt-get update \
    && apt-get upgrade -y \
    && apt-get install -y docker-ce docker-ce-cli \
    && usermod -aG docker ${NON_ROOT_CONTAINER_USER} \
    && curl -L "${DOCKER_COMPOSE_BASE_DOWNLOAD_URL}/${DOCKER_COMPOSE_VERSION}/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose \
    && chmod +x /usr/local/bin/docker-compose \
    && apt clean

# Switch to non root user
USER $NON_ROOT_CONTAINER_USER
WORKDIR /home/${NON_ROOT_CONTAINER_USER}
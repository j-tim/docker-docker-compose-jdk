FROM adoptopenjdk/openjdk11-openj9:jdk-11.0.9_11_openj9-0.23.0

# Default to UTF-8 file.encoding
ENV LANG C.UTF-8

ENV DOCKER_HOST tcp://docker:2375/

# Setup the non root user and group
ENV NON_ROOT_CONTAINER_USER bob-the-builder
ENV DOCKER_VERSION 5:20.10.5~3-0~ubuntu-focal
ENV DOCKER_COMPOSE_VERSION 1.28.6
ENV DOCKER_COMPOSE_BASE_DOWNLOAD_URL https://github.com/docker/compose/releases/download
ENV PACK_VERSION=v0.18.0

RUN groupadd ${NON_ROOT_CONTAINER_USER} \
    && useradd -rm -d /home/${NON_ROOT_CONTAINER_USER} -s /bin/bash -g 1000 -G ${NON_ROOT_CONTAINER_USER} -u 1000 ${NON_ROOT_CONTAINER_USER}

RUN apt update \
    && apt install -y apt-transport-https ca-certificates curl jq gnupg-agent software-properties-common \
    && curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add - \
    && add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" \
    && apt-get update \
    && apt-get upgrade -y \
    && apt-get install -y docker-ce=${DOCKER_VERSION} docker-ce-cli=${DOCKER_VERSION} \
    && usermod -aG docker ${NON_ROOT_CONTAINER_USER} \
    && curl -L "${DOCKER_COMPOSE_BASE_DOWNLOAD_URL}/${DOCKER_COMPOSE_VERSION}/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose \
    && chmod +x /usr/local/bin/docker-compose \
    && apt clean \
    && (curl -sSL "https://github.com/buildpacks/pack/releases/download/$PACK_VERSION/pack-$PACK_VERSION-linux.tgz" | tar -C /usr/local/bin/ --no-same-owner -xzv pack)

# Switch to non root user
USER $NON_ROOT_CONTAINER_USER
WORKDIR /home/${NON_ROOT_CONTAINER_USER}
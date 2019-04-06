FROM adoptopenjdk/openjdk11:jdk-11.0.2.9

# Default to UTF-8 file.encoding
ENV LANG C.UTF-8

# Setup the non root user and group
ENV NON_ROOT_CONTAINER_USER bob-the-builder
ENV DOCKER_COMPOSE_VERSION 1.23.2
ENV DOCKER_COMPOSE_BASE_DOWNLOAD_URL https://github.com/docker/compose/releases/download

RUN groupadd -g 1000 ${NON_ROOT_CONTAINER_USER} && \
    useradd -u 1000 ${NON_ROOT_CONTAINER_USER} -g ${NON_ROOT_CONTAINER_USER}

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
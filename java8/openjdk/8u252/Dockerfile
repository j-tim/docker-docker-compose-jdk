FROM jtim/docker-docker-compose:20.10.2-compose-1.28.0

# Default to UTF-8 file.encoding
ENV LANG C.UTF-8

USER root

# add a simple script that can auto-detect the appropriate JAVA_HOME value
# based on whether the JDK or only the JRE is installed
RUN { \
		echo '#!/bin/sh'; \
		echo 'set -e'; \
		echo; \
		echo 'dirname "$(dirname "$(readlink -f "$(which javac || which java)")")"'; \
	} > /usr/local/bin/docker-java-home \
	&& chmod +x /usr/local/bin/docker-java-home
ENV JAVA_HOME /usr/lib/jvm/java-1.8-openjdk
ENV PATH $PATH:/usr/lib/jvm/java-1.8-openjdk/jre/bin:/usr/lib/jvm/java-1.8-openjdk/bin

# https://pkgs.alpinelinux.org/packages?name=openjdk8&branch=v3.12
ENV JAVA_VERSION 8u252
ENV JAVA_ALPINE_VERSION 8.252.09-r0

ENV DOCKER_HOST tcp://docker:2375
ENV DOCKER_DRIVER overlay2
ENV DOCKER_TLS_CERTDIR ""

RUN set -x \
    && apk update \
    && apk upgrade \
	&& apk add --no-cache \
		openjdk8="$JAVA_ALPINE_VERSION" \
	&& [ "$JAVA_HOME" = "$(docker-java-home)" ]

USER bob-the-builder
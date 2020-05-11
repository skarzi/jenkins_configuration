FROM jenkins/slave:4.3-4

ARG DOCKER_GID

ENV DOCKER_GID=${DOCKER_GID}

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

USER root
# install docker dependencies
RUN apt-get -qq update \
    && apt-get \
        -qqy --no-install-recommends \
        install \
            apt-transport-https \
            ca-certificates \
            curl \
            gnupg2 \
            software-properties-common \
    && rm -rf /var/lib/apt/lists/* \
    && apt-get -qq -y clean
# add docker apt repository
RUN curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -
RUN add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/debian \
   $(lsb_release -cs) \
   stable"
# install docker and docker-compose
# TODO: allow to install specific version of docker and docker-compose
RUN apt-get -qq update \
    && apt-get \
        -qqy --no-install-recommends \
        install \
            docker-ce \
    && rm -rf /var/lib/apt/lists/* \
    && apt-get -qq -y clean \
    && curl -L \
        "https://github.com/docker/compose/releases/download/1.25.5/docker-compose-$(uname -s)-$(uname -m)" \
        -o /usr/local/bin/docker-compose \
    && chmod +x /usr/local/bin/docker-compose

# NOTE: `jenkins` user need to be `sudo` user or member of`docker` group to
# has proper permissions to use docker. Docker's socket is mounted as
# volume from host's socket, so `docker` group must have the same `GID` as
# host's  `docker` group
RUN groupmod --gid ${DOCKER_GID} docker && usermod -aG docker jenkins

USER jenkins

ARG BASE_ARCH

FROM vlrpi/teamcity-server-${BASE_ARCH}:debian-bullseye-2021.2
LABEL maintainer="Vova Lantsov"
LABEL contact_email="contact@vova-lantsov.dev"
LABEL telegram="https://t.me/vova_lantsov"

ARG DOCKER_ARCH

ADD buildAgent.properties TeamCity/buildAgent/conf/

RUN apt-get install -y git curl zlib1g liblttng-ust0 apt-transport-https gnupg-agent software-properties-common
RUN apt-get upgrade -y

RUN curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -

RUN add-apt-repository \
    "deb [arch=${DOCKER_ARCH}] https://download.docker.com/linux/debian bullseye stable"

RUN apt-get update
RUN apt-get install -y docker-ce docker-ce-cli containerd.io

RUN curl -L "https://github.com/linuxserver/docker-docker-compose/releases/download/1.29.2-ls51/docker-compose-${DOCKER_ARCH}" -o /usr/bin/docker-compose
RUN chmod +x /usr/bin/docker-compose

EXPOSE 8111 9090
ENTRYPOINT ["TeamCity/buildAgent/bin/agent.sh","run"]
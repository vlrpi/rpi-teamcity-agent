ARG BASE_ARCH

FROM vlrpi/teamcity-server-${BASE_ARCH}:ubuntu-jammy-2022.10
LABEL maintainer="Vova Lantsov"
LABEL contact_email="contact@vova-lantsov.dev"
LABEL telegram="https://t.me/vova_lantsov"

ARG DOCKER_ARCH

ADD buildAgent.properties TeamCity/buildAgent/conf/

RUN [ "cross-build-start" ]

RUN apt-get install -y git curl zlib1g apt-transport-https gnupg-agent software-properties-common liblttng-ust1
RUN apt-get upgrade -y

RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

RUN add-apt-repository \
    "deb [arch=${DOCKER_ARCH}] https://download.docker.com/linux/ubuntu jammy stable"

RUN apt-get update
RUN apt-get install -y docker-ce docker-ce-cli containerd.io

RUN curl -L "https://github.com/docker/compose/releases/download/v2.20.2/docker-compose-linux-${DOCKER_ARCH}" -o /usr/bin/docker-compose
RUN chmod +x /usr/bin/docker-compose

RUN [ "cross-build-end" ]

EXPOSE 8111 9090
ENTRYPOINT ["TeamCity/buildAgent/bin/agent.sh","run"]
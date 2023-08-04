ARG BASE_ARCH

FROM vlrpi/teamcity-server-${BASE_ARCH}:ubuntu-bionic-2023.05
LABEL maintainer="Vova Lantsov"
LABEL contact_email="contact@vova-lantsov.dev"
LABEL telegram="https://t.me/vova_lantsov"

ARG DOCKER_ARCH

ADD buildAgent.properties TeamCity/buildAgent/conf/

RUN [ "cross-build-start" ]

RUN apt-get install -y ca-certificates curl gnupg git zlib1g apt-transport-https software-properties-common liblttng-ust0

RUN install -m 0755 -d /etc/apt/keyrings
RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | gpg --dearmor -o /etc/apt/keyrings/docker.gpg
RUN chmod a+r /etc/apt/keyrings/docker.gpg

RUN echo "deb [arch=${DOCKER_ARCH} signed-by=/etc/apt/keyrings/docker.gpg] \
    https://download.docker.com/linux/ubuntu bionic stable" | \
    tee /etc/apt/sources.list.d/docker.list > /dev/null

RUN apt-get update
RUN apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

RUN [ "cross-build-end" ]

EXPOSE 8111 9090
ENTRYPOINT ["TeamCity/buildAgent/bin/agent.sh","run"]
FROM vlrpi/rpi-teamcity-server:ubuntu-focal-2020.1
LABEL maintainer="Vova Lantsov"
LABEL contact_email="contact@vova-lantsov.dev"
LABEL telegram="https://t.me/vova_lantsov"

ADD buildAgent.properties TeamCity/buildAgent/conf/

RUN apt-get install -y git curl zlib1g liblttng-ust0 apt-transport-https gnupg-agent software-properties-common
RUN apt-get upgrade -y

RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

RUN add-apt-repository \
   "deb [arch=arm64] https://download.docker.com/linux/ubuntu focal stable"

RUN apt-get update
RUN apt-get install -y docker-ce docker-ce-cli containerd.io

RUN apt-get upgrade -y

RUN curl -L "https://github.com/linuxserver/docker-docker-compose/releases/download/1.28.5-ls33/docker-compose-arm64" -o /usr/bin/docker-compose
RUN chmod +x /usr/bin/docker-compose

EXPOSE 8111 9090
ENTRYPOINT TeamCity/buildAgent/bin/agent.sh run
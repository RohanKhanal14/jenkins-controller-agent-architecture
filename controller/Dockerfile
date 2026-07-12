FROM jenkins/jenkins:lts-jdk21

USER root

RUN apt-get update && apt-get install -y \
    curl \
    git \
    vim \
    ca-certificates \
    iputils-ping \
    iproute2 \
    && rm -rf /var/lib/apt/lists/*

USER jenkins

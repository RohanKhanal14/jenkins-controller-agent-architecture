FROM ubuntu:24.04

ARG JENKINS_AGENT_USER=jenkins
ARG JENKINS_AGENT_HOME=/home/jenkins

USER root

RUN apt-get update && apt-get install -y \
    openssh-server \
    openjdk-21-jdk \
    git \
    curl \
    wget \
    unzip \
    bash \
    sudo \
    ca-certificates \
    gnupg \
    lsb-release \
    docker.io \
    nodejs \
    npm \
    && rm -rf /var/lib/apt/lists/*

RUN useradd -m -d ${JENKINS_AGENT_HOME} -s /bin/bash ${JENKINS_AGENT_USER}

RUN mkdir -p /var/run/sshd \
    && mkdir -p ${JENKINS_AGENT_HOME}/.ssh \
    && chmod 700 ${JENKINS_AGENT_HOME}/.ssh \
    && chown -R ${JENKINS_AGENT_USER}:${JENKINS_AGENT_USER} ${JENKINS_AGENT_HOME}/.ssh

COPY ssh/jenkins_agent_key.pub ${JENKINS_AGENT_HOME}/.ssh/authorized_keys

RUN chmod 600 ${JENKINS_AGENT_HOME}/.ssh/authorized_keys \
    && chown ${JENKINS_AGENT_USER}:${JENKINS_AGENT_USER} ${JENKINS_AGENT_HOME}/.ssh/authorized_keys

RUN usermod -aG docker ${JENKINS_AGENT_USER}

RUN echo "${JENKINS_AGENT_USER} ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/jenkins-agent \
    && chmod 0440 /etc/sudoers.d/jenkins-agent

EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]

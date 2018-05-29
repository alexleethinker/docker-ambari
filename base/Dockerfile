FROM ubuntu:16.04
MAINTAINER Alex Lee

USER root

ENV LANG en_US.UTF-8

# install dev tools
COPY ambari.list /etc/apt/sources.list.d/ambari.list
RUN apt-key adv --recv-keys --keyserver keyserver.ubuntu.com B9733A7A07513CAD && \
    apt-get update -y && \
    apt-get install -y curl tar sudo ssh rsync ntp unzip \ 
                       openjdk-8-jdk && \
    update-rc.d ntp defaults  && \
    apt-get clean

# passwordless ssh
COPY sshd_config /etc/ssh/sshd_config
COPY ssh_config /etc/ssh/ssh_config
RUN service ssh restart && \
    rm -f /etc/ssh/ssh_host_dsa_key /etc/ssh/ssh_host_rsa_key /root/.ssh/id_rsa && \
    mkdir /root/.ssh && \
    ssh-keygen -q -N "" -t dsa -f /etc/ssh/ssh_host_dsa_key && \
    ssh-keygen -q -N "" -t rsa -f /etc/ssh/ssh_host_rsa_key && \
    ssh-keygen -q -N "" -t rsa -f /root/.ssh/id_rsa && \
    cat /root/.ssh/id_rsa.pub >> /root/.ssh/authorized_keys && \
    chmod 700 /root/.ssh && \
    chmod 600 /root/.ssh/authorized_keys && \
    chmod 600 /root/.ssh/id_rsa && \
    chmod 600 /root/.ssh/id_rsa.pub


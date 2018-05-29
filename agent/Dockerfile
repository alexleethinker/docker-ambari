FROM ambari-base
MAINTAINER Alex Lee

USER root

# install dev tools
RUN apt-get install -y ambari-agent
COPY ambari-agent.ini /etc/ambari-agent/conf/ambari-agent.ini

ENTRYPOINT service ssh restart && service ntp restart && ambari-agent start && bash

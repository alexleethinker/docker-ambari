FROM ambari-base
MAINTAINER Alex Lee

USER root

# install dev tools
RUN apt-get install -y ambari-server libmysql-java && \
    apt-get clean && \
    chmod 644 /usr/share/java/mysql-connector-java.jar && \
    ambari-server setup --jdbc-db=mysql --jdbc-driver=/usr/share/java/mysql-connector-java.jar

ENTRYPOINT ambari-server setup -j /usr/lib/jvm/java-8-openjdk-amd64 -s && service ntp restart && service ssh restart && ambari-server start && bash

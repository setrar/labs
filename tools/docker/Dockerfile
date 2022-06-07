FROM ubuntu:latest

RUN apt-get update && apt-get -y upgrade
RUN apt-get -y install curl
RUN apt-get -y install default-jre

RUN curl -O http://archive.apache.org/dist/activemq/5.16.2/apache-activemq-5.16.2-bin.tar.gz
RUN mkdir -p /opt/apache/activemq
RUN tar xvzf apache-activemq-5.16.2-bin.tar.gz -C /opt/apache/activemq

WORKDIR /opt/apache/activemq/apache-activemq-5.16.2/bin
VOLUME /opt/apache/activemq/apache-activemq-5.16.2/conf

RUN echo './activemq start && tail -f /opt/apache/activemq/apache-activemq-5.16.2/data/activemq.log' > start.sh

# Admin interface
EXPOSE 8161
# Active MQ's default port (Listen port)
EXPOSE 61616

ENTRYPOINT ["./activemq","console","-Djetty.host=0.0.0.0"]

#CMD ["/bin/bash", "./start.sh"]
 

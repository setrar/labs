FROM ubuntu:20.04

RUN apt-get update \
    && apt-get install -y --no-install-recommends curl \
    && rm -rf /var/lib/apt/lists/*

RUN mkdir /opt/tomcat/

WORKDIR /opt/tomcat
RUN curl -k -O https://dlcdn.apache.org/tomcat/tomcat-8/v8.5.79/bin/apache-tomcat-8.5.79.tar.gz
RUN tar xvfz apache*.tar.gz
RUN mv apache-tomcat-8.5.79/* /opt/tomcat/.

RUN \
  apt-get update && \
  DEBIAN_FRONTEND=noninteractive \
    apt-get -y install \
      default-jre-headless \
  && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/*

RUN java -version

WORKDIR /opt/tomcat/webapps
COPY target/jms-webapp.war .

EXPOSE 8080

CMD ["/opt/tomcat/bin/catalina.sh", "run"]

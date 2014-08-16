FROM tifayuki/java:java7
MAINTAINER Feng Honglin <hfeng@tutum.co>

ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && \
  apt-get install -yq wget pwgen && \
  rm -rf /var/lib/apt/lists/*

ENV TOMCAT_MAJOR_VERSION 7
ENV TOMCAT_MINOR_VERSION 7.0.54
ENV CATALINA_HOME /tomcat

# INSTALL TOMCAT
RUN wget -q https://archive.apache.org/dist/tomcat/tomcat-${TOMCAT_MAJOR_VERSION}/v${TOMCAT_MINOR_VERSION}/bin/apache-tomcat-${TOMCAT_MINOR_VERSION}.tar.gz && \
  tar zxf apache-tomcat-*.tar.gz && \
  rm apache-tomcat-*.tar.gz && \
  mv apache-tomcat* tomcat

ADD create_tomcat_admin_user.sh /create_tomcat_admin_user.sh
ADD run.sh /run.sh
RUN chmod +x /*.sh

EXPOSE 8080
CMD ["/run.sh"]
# Pull base image.
FROM dockerfile/java:oracle-java7

RUN apt-get update && \
    apt-get install -yq --no-install-recommends wget pwgen ca-certificates && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

ENV TOMCAT_MAJOR_VERSION 7
ENV TOMCAT_MINOR_VERSION 7.0.55
ENV CATALINA_HOME /tomcat

RUN mkdir -p /tomcat
RUN mkdir -p /tmp/tomcat

WORKDIR /tmp/tomcat

# INSTALL TOMCAT
RUN wget -q https://archive.apache.org/dist/tomcat/tomcat-${TOMCAT_MAJOR_VERSION}/v${TOMCAT_MINOR_VERSION}/bin/apache-tomcat-${TOMCAT_MINOR_VERSION}.tar.gz && \
    wget -qO- https://archive.apache.org/dist/tomcat/tomcat-${TOMCAT_MAJOR_VERSION}/v${TOMCAT_MINOR_VERSION}/bin/apache-tomcat-${TOMCAT_MINOR_VERSION}.tar.gz.md5 | md5sum -c - && \
    tar zxf apache-tomcat-*.tar.gz && \
    rm apache-tomcat-*.tar.gz && \    
    mv /tmp/tomcat/apache-tomcat*/* /tomcat

WORKDIR ${CATALINA_HOME}

VOLUME ["/tomcat/webapps","/tomcat/logs","/tomcat/conf"]

ADD create_tomcat_admin_user.sh ${CATALINA_HOME}/create_tomcat_admin_user.sh
ADD run.sh ${CATALINA_HOME}/run.sh
RUN chmod +x ${CATALINA_HOME}/*.sh

RUN ln -s ${CATALINA_HOME}/run.sh /run.sh

EXPOSE 8080
CMD ["/run.sh"]


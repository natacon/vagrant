#FROM tomcat:9.0.30-jdk13-openjdk-oracle
FROM centos:latest

RUN yum install -y wget

RUN mkdir -p /opt/jdk
RUN mkdir -p /usr/local/tomcat

RUN mkdir -p /var/log/lip
RUN mkdir -p /etc/lip
RUN mkdir -p /app
RUN mkdir -p /var/log/lip/webapp

WORKDIR /var/log/lip/webapp
RUN mkdir access batch jdbc mail maintenance naw pool reference rireki service transaction

RUN wget -O - -q --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" \
 https://download.oracle.com/otn-pub/java/jdk/13.0.2+8/d4173c853231432d94f001e99d882ca7/jdk-13.0.2_linux-x64_bin.tar.gz \
 | tar xzf - -C /opt/jdk

RUN wget -O - -q http://ftp.yz.yamagata-u.ac.jp/pub/network/apache/tomcat/tomcat-9/v9.0.31/bin/apache-tomcat-9.0.31.tar.gz \
 | tar xzf - -C /usr/local/tomcat --strip-components 1

ENV JAVA_HOME=/opt/jdk/jdk-13.0.2
ENV CATALINA_HOME=/usr/local/tomcat
ENV PATH $CATALINA_HOME/bin:$JAVA_HOME/bin:$PATH

COPY ./tomcat/jasper.jar $CATALINA_HOME/lib
COPY ./tomcat/tomcat-users.xml $CATALINA_HOME/conf
COPY ./tomcat/manager/context.xml $CATALINA_HOME/webapps/manager/META-INF

WORKDIR $CATALINA_HOME
CMD ["catalina.sh", "run"]

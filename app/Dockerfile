FROM ubuntu:18.04 AS build
RUN apt-get update; \
    apt-get install -y maven; \
COPY . ./
WORKDIR app
RUN mvn package

FROM ubuntu:18.04
RUN apt-get update; \
    apt-get install -y curl; \
    apt-get install -y default-jdk;
WORKDIR /opt/tomcat
RUN curl -O https://apache-mirror.rbc.ru/pub/apache/tomcat/tomcat-8/v8.5.56/bin/apache-tomcat-8.5.56.tar.gz; \
    tar xvfz apache-tomcat-8.5.56.tar.gz; \
    mv apache-tomcat-8.5.56/* /opt/tomcat/ 
COPY --from=build /app/target/*.war /opt/tomcat/webapps/
EXPOSE 8080
CMD ["/opt/tomcat/bin/catalina.sh", "run"]


# first
#FROM maven:3-jdk-7-alpine as build
#COPY . ./
#WORKDIR app
#RUN mvn package
#
# second
#FROM tomcat:8.0-jre7-alpine
#COPY --from=build /app/target/*.war /usr/local/tomcat/webapps/
#EXPOSE 8080

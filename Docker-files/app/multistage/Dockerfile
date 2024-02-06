FROM openjdk:11 AS BUILD_IMAGE
RUN apt update && apt install maven -y
RUN git clone https://github.com/udit-1211/ci-docker.git
RUN ci-docker && git checkout docker && mvn install

FROM tomcat:9-jre11

RUN rm -rf /var/lib/tomcat9/webapps/*

COPY --from=BUILD_IMAGE ci-docker/target/vprofile-v2.war /var/lib/tomcat9/webapps/ROOT.war

EXPOSE 8080
CMD ["catalina.sh", "run"]

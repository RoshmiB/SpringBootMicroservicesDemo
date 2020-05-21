FROM openjdk:8-jdk-alpine
COPY ./target/ProfileMicroserviceProducer-0.0.1-SNAPSHOT.war ProfileMicroserviceProducer-0.0.1-SNAPSHOT.war
ENV JAVA_OPTS=""
CMD [ "sh", "-c", "java $JAVA_OPTS -jar ProfileMicroserviceProducer-0.0.1-SNAPSHOT.war" ]
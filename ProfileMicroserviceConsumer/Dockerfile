FROM openjdk:8-jdk-alpine
COPY ./target/ProfileMicroserviceConsumer-0.0.1-SNAPSHOT.war ProfileMicroserviceConsumer-0.0.1-SNAPSHOT.war
ENV JAVA_OPTS=""
CMD [ "sh", "-c", "java $JAVA_OPTS -jar ProfileMicroserviceConsumer-0.0.1-SNAPSHOT.war" ]
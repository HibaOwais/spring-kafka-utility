#Build Stage
FROM gradle:7.3.1-jdk8 AS build
COPY --chown=gradle:gradle . /home/gradle/src
WORKDIR /home/gradle/src
RUN gradle build

#RUN stage
FROM openjdk:8-jre-slim
EXPOSE 8000 5005 9091
RUN mkdir /app
COPY --from=build /home/gradle/src/build/libs/*.jar /app/service-b.jar
MAINTAINER junaidshakeel
ENTRYPOINT ["java","-jar","-agentlib:jdwp=transport=dt_socket,server=y,address=8000,suspend=n","/app/service-b.jar"]
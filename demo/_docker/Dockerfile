FROM maven:3.8.3-openjdk-17 as maven_build
ENV HOME=/demo
RUN mkdir -p $HOME
WORKDIR $HOME
ADD pom.xml $HOME
RUN mvn verify --fail-never
ADD ./ $HOME
RUN mvn package

FROM openjdk:17-jdk-slim
WORKDIR $HOME
COPY --from=maven_build /demo/target/demo-0.0.1-SNAPSHOT.jar app.jar

EXPOSE 8080
CMD exec java \
    -jar app.jar


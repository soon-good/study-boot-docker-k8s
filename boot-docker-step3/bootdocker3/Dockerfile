FROM openjdk:11.0.8-jdk-slim AS openjdk-image
RUN apt-get update;
WORKDIR source
ARG JAR_FILE=target/bootdocker*.jar
COPY ${JAR_FILE} application.jar
RUN jar -xf ./application.jar

FROM openjdk:11.0.8-jre-slim
WORKDIR application
COPY --from=openjdk-image source/BOOT-INF/lib lib
COPY --from=openjdk-image source/BOOT-INF/classes app
ENTRYPOINT ["java","-cp","app:lib/*", "io.study.bootdocker.BootdockerApplication"]

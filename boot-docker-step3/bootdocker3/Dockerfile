FROM openjdk:11.0.8-jdk-slim AS openjdk-image
WORKDIR original
ARG JAR_FILE=target/bootdocker*.jar
COPY ${JAR_FILE} target.jar
RUN java -jar -Djarmode=layertools target.jar extract

FROM openjdk:11.0.8-jre-slim
WORKDIR application
COPY --from=openjdk-image original/application ./
COPY --from=openjdk-image original/dependencies ./
COPY --from=openjdk-image original/snapshot-dependencies ./
COPY --from=openjdk-image original/spring-boot-loader ./
ENTRYPOINT ["java", "org.springframework.boot.loader.JarLauncher"]

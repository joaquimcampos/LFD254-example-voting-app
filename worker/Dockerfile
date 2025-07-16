FROM jcampos15/worker-base:v1 AS build
WORKDIR /code
COPY . .
RUN mvn package -D skipTests && \
  mv target/worker-jar-with-dependencies.jar /worker.jar

FROM build AS test
CMD ["mvn", "clean", "test"]

FROM openjdk:8-jre-alpine AS run
WORKDIR /run
COPY --from=build /worker.jar ./
CMD ["java", "-jar", "worker.jar"]

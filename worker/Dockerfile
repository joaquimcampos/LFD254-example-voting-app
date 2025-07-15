FROM maven:3.5-jdk-8-alpine AS build
WORKDIR /code
COPY . .
RUN mvn package -D skipTests && \
  mv target/worker-jar-with-dependencies.jar /artifact.jar

FROM build AS test
CMD ["mvn", "clean", "test"]

FROM openjdk:8-jre-alpine AS run
WORKDIR /run
COPY --from=build /artifact.jar ./
CMD ["java", "-jar", "artifact.jar"]

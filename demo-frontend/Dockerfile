# Use the official maven/Java 8 image to create a build artifact.
# https://hub.docker.com/_/maven
FROM maven:3.6.3-jdk-8 as builder

# Copy local code to the container image.
WORKDIR /app
COPY pom.xml .
COPY src ./src

# Build a release artifact.
RUN mvn package -DskipTests

FROM openjdk:8-jdk-alpine

VOLUME /tmp
COPY --from=builder /app/target/demo-frontend-*.jar /demo-frontend.jar

# Run the app in the container.
ENTRYPOINT exec java -jar /demo-frontend.jar --debug

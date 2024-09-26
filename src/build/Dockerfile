# Use a base image with JDK
FROM openjdk:17-jdk-slim

# Set the working directory
WORKDIR /app

# Copy the JAR file of your Spring Boot application
COPY target/my-spring-boot-app-0.0.1-SNAPSHOT.jar app.jar

# Define the version of the OpenTelemetry Java Agent you want to download
ENV OTEL_AGENT_VERSION=1.30.0
# Download the OpenTelemetry Java Agent
RUN apt-get update && apt-get install -y curl && \
    curl -L -o opentelemetry-javaagent.jar https://github.com/open-telemetry/opentelemetry-java-instrumentation/releases/download/v$OTEL_AGENT_VERSION/opentelemetry-javaagent.jar && \
    chmod 644 opentelemetry-javaagent.jar

# Run the application with the Java Agent
ENTRYPOINT ["java", "-javaagent:/app/opentelemetry-javaagent.jar", "-jar", "/app/app.jar"]

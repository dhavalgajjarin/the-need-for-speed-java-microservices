# Stage 1: Create custom JRE with jlink
FROM eclipse-temurin:21-jdk-alpine-3.22 AS builder

# Install binutils for objcopy (required by jlink)
RUN apk add --no-cache binutils

# Analyze the JAR to determine required modules
WORKDIR /app
COPY target/*.jar .
RUN rm -rf original*.jar
RUN mv *.jar app.jar

# List modules and create custom JRE
RUN jdeps \
    --ignore-missing-deps \
    --print-module-deps \
    --multi-release 21 \
    app.jar > /tmp/modules.txt

# Create optimized JRE with jlink
RUN jlink \
    --add-modules $(cat /tmp/modules.txt),jdk.crypto.ec,java.logging,java.xml,java.desktop,java.management,java.naming,java.security.jgss,java.instrument,java.sql,jdk.zipfs  \
    --strip-debug \
    --no-man-pages \
    --no-header-files \
    --compress=2 \
    --output /custom-jre

# Stage 2: Final runtime image
FROM alpine:3.22

# Install runtime dependencies
RUN apk add --no-cache \
    ca-certificates \
    curl \
    gcompat \
    tzdata

# Copy custom JRE
COPY --from=builder /custom-jre /opt/java

# Set environment variables
ENV JAVA_HOME=/opt/java
ENV PATH="${JAVA_HOME}/bin:${PATH}"

WORKDIR /app

# Copy Spring Boot layers in order of least to most frequently changing
COPY --from=builder /app/app.jar ./

# Expose port
EXPOSE 8080

# Set JVM options for containerized environment
ENV JAVA_OPTS="-XX:+UseContainerSupport -XX:MaxRAMPercentage=75.0"

# Run the application
ENTRYPOINT ["sh", "-c", "java $JAVA_OPTS -jar app.jar"]
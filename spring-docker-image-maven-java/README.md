## Spring Boot 3.3.x Documentation

- [User Guide](https://docs.spring.io/spring-boot/docs/current/reference/html/)
- [API Reference (Javadoc)](https://docs.spring.io/spring-boot/docs/current/api/)
- [Spring Boot Configuration Reference](https://docs.spring.io/spring-boot/docs/current/reference/html/application-properties.html)
- [Spring Guides](https://spring.io/guides)
---

## Build & Plugin Documentation

### 🔧 Spring Boot Maven Plugin

- [Spring Boot Maven Plugin Documentation](https://docs.spring.io/spring-boot/docs/current/maven-plugin/reference/html/)

Used to package, run, and build Docker images for Spring Boot applications.

### 🧹 Spotless Plugin

- [Spotless Code Formatter](https://github.com/diffplug/spotless)

Used for code style and formatting checks.

### 🧩 Maven Enforcer Plugin

- [Maven Enforcer Plugin](https://maven.apache.org/enforcer/maven-enforcer-plugin/)

Ensures consistent Maven setup and dependency rules.

## Advanced Features

### 🚀 AOT (Ahead-of-Time Processing)

- [Spring AOT & Native Image Support](https://docs.spring.io/spring-boot/docs/current/reference/html/native-image.html)

Spring Boot provides AOT processing and GraalVM native image support for fast startup and reduced memory footprint.

### ⚡ CRaC (Coordinated Restore at Checkpoint)

- [Spring CRaC Support Documentation](https://docs.spring.io/spring-boot/docs/current/reference/html/advanced-features.html#advanced-features.crac)

- [OpenJDK CRaC Project](https://wiki.openjdk.org/display/CRaC)

Enables fast startup and state restoration for JVM-based applications.

### 📦 JSON Serialization (Jackson)

- [Spring Boot Jackson Integration](https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/#howto.spring-mvc.customize-jackson-objectmapper)

Spring Boot provides auto-configuration for Jackson JSON processing, used for REST controllers and data serialization.

## Commands

> **Note**  
> While building image using maven plugin if you get the error `Execution default-cli of goal org.springframework.boot:spring-boot-maven-plugin:3.5.7:build-image failed: No 'io.buildpacks.builder.metadata' label found in image config labels ''`
> then you have issue with builder image so you need to clean all in docker to run it properly. `docker system prune --all`

### Docker image using jib-magen-plugin

```bash
./mvnw clean package jib:dockerBuild -Djib.to.image=spring-docker:jib
./ttfr.sh spring-docker:jib
```

### Docker image using spring-boot-maven-plugin

```bash
./mvnw clean spring-boot:build-image -Dspring-boot.build-image.imageName=spring-docker:boot
./ttfr.sh spring-docker:boot
```

### Docker image using Dockerfile and jlink

```bash
./mvnw clean package
docker build -t spring-docker:slim .
./ttfr.sh spring-docker:slim
```

### Docker image with a GraalVM native executable inside

```bash
./mvnw clean spring-boot:build-image -Pnative -Dspring-boot.build-image.imageName=spring-docker:boot-native
./ttfr.sh spring-docker:boot-native
```

### Docker image using Dockerfile with a GraalVM native executable inside

```bash
./mvnw clean native:compile -Pnative
docker build -f Dockerfile.native -t spring-docker:native .
./ttfr.sh spring-docker:native
```
## Micronaut 4.10.1 Documentation

- [User Guide](https://docs.micronaut.io/4.10.1/guide/index.html)
- [API Reference](https://docs.micronaut.io/4.10.1/api/index.html)
- [Configuration Reference](https://docs.micronaut.io/4.10.1/guide/configurationreference.html)
- [Micronaut Guides](https://guides.micronaut.io/index.html)
---

## Build & Plugin Documentation

### 🔧 Micronaut Maven Plugin

- [Micronaut Maven Plugin](https://micronaut-projects.github.io/micronaut-maven-plugin/latest/)

Used to package, run, and build Docker images for Micronaut applications.

### 🧹 Spotless Plugin

- [Spotless Code Formatter](https://github.com/diffplug/spotless)

Used for code style and formatting checks.

### 🧩 Maven Enforcer Plugin

- [Maven Enforcer Plugin](https://maven.apache.org/enforcer/maven-enforcer-plugin/)

Ensures consistent Maven setup and dependency rules.

## Advanced Features

### 🚀 AOT (Ahead-of-Time Processing)

- [Micronaut AOT](https://micronaut-projects.github.io/micronaut-aot/latest/guide/)

### ⚡ CRaC (Coordinated Restore at Checkpoint)

- [Micronaut Support for CRaC (Coordinated Restore at Checkpoint) documentation](https://micronaut-projects.github.io/micronaut-crac/latest/guide)

- [https://wiki.openjdk.org/display/CRaC](https://wiki.openjdk.org/display/CRaC)

### 📦 JSON Serialization (Jackson)

- [Micronaut Serialization Jackson Core](https://micronaut-projects.github.io/micronaut-serialization/latest/guide/)

## Commands

### Docker Image

```bash
./mvnw clean package -Dpackaging=docker -Djib.to.image=micronaut-docker:jib
./ttfr.sh micronaut-docker:jib
```

### Docker image using Dockerfile and jlink

```bash
./mvnw clean package
docker build -t micronaut-docker:slim .
./ttfr.sh micronaut-docker:slim
```

### Docker image with a GraalVM native executable inside

```bash
./mvnw clean package -Dpackaging=docker-native -Pgraalvm -Djib.to.image=micronaut-docker:native
./ttfr.sh micronaut-docker:native
```

### CRaC Docker Image

```bash
./mvnw clean package -Dpackaging=docker-crac -Djib.to.image=micronaut-docker:crac
./ttfr.sh micronaut-docker:crac
```

### AOT Optimized Docker Image

```bash
./mvnw clean package -Dpackaging=docker -Dmicronaut.aot.enabled=true -Djib.to.image=micronaut-docker:aot
./ttfr.sh micronaut-docker:aot
```

### AOT Optimized Docker Image with a native executable inside

```bash
./mvnw clean package -Dpackaging=docker-native -Dmicronaut.aot.enabled=true -Pgraalvm -Djib.to.image=micronaut-docker:aot-native
./ttfr.sh micronaut-docker:aot-native
```
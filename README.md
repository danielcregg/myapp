# MyApp - Vert.x HTTP ConfigMap Booster

![Java](https://img.shields.io/badge/Java-ED8B00?style=flat-square&logo=openjdk&logoColor=white)
![Vert.x](https://img.shields.io/badge/Vert.x-782A90?style=flat-square&logo=eclipse-vertx&logoColor=white)
![OpenShift](https://img.shields.io/badge/OpenShift-EE0000?style=flat-square&logo=redhatopenshift&logoColor=white)
![License: Apache 2.0](https://img.shields.io/badge/License-Apache%202.0-blue.svg?style=flat-square)

An Eclipse Vert.x booster application demonstrating externalized configuration using OpenShift ConfigMaps. The application exposes a simple HTTP greeting endpoint whose message template and log level are dynamically loaded from a Kubernetes ConfigMap.

## Overview

This project showcases how to leverage OpenShift ConfigMaps for runtime application configuration with Eclipse Vert.x. The application periodically polls for configuration changes, allowing message templates and logging levels to be updated without redeployment. It serves as a practical example of the externalized configuration pattern in cloud-native Java microservices.

## Features

- **Dynamic configuration** loaded from OpenShift ConfigMaps at runtime
- **Periodic config polling** that detects and applies changes every 2 seconds
- **RESTful greeting endpoint** with customizable name parameter
- **Health check endpoint** at `/health` for container orchestration readiness
- **Static web UI** with a form-based interface for invoking the greeting service
- **Configurable log levels** that can be changed without restarting the application

## Prerequisites

- Java 8 JDK or later
- Apache Maven 3.3.x or later
- OpenShift cluster (Minishift or Red Hat CDK) for ConfigMap functionality

## Getting Started

### Installation

```bash
git clone https://github.com/danielcregg/myapp.git
cd myapp
```

### Usage

**Run locally:**

```bash
mvn compile vertx:run
```

Then visit `http://localhost:8080` or use curl:

```bash
curl http://localhost:8080/api/greeting
curl http://localhost:8080/api/greeting?name=Sarah
```

**Deploy to OpenShift:**

```bash
oc login -u developer -p developer
oc new-project my-project
oc create configmap app-config --from-file=app-config.yml
mvn clean fabric8:deploy -Popenshift
```

## Tech Stack

| Technology | Purpose |
|---|---|
| Java 8 | Core programming language |
| Eclipse Vert.x 3.5 | Reactive toolkit and HTTP server |
| Vert.x Config | Externalized configuration management |
| Fabric8 Maven Plugin | OpenShift deployment automation |
| Arquillian Cube | Integration testing on OpenShift |

## License

This project is licensed under the Apache License 2.0. See the [LICENSE](LICENSE) file for details.

# Application Development Lifecycle with Maven, SonarQube, GitHub Actions, and Docker

##  Lifecycle Overview

1. **Development Phase**
    - Developers write code (e.g., Java).
    - Build locally with Maven:
      ```bash
      mvn clean install
      ```
    - Run local unit tests.

2. **Version Control (GitHub)**
    - Push code to GitHub.
    - Create Pull Requests (PRs).

3. **CI/CD Automation (GitHub Actions)**
    - Trigger GitHub Actions workflow on `push` or `pull_request`.
    - Steps:
      - Checkout code
      - Set up JDK
      - Build and test using Maven
      - Run SonarQube analysis
      - Build Docker container
      - (Optional) Push Docker container to registry

4. **Quality Assurance (SonarQube)**
    - Analyze code for:
      - Bugs
      - Vulnerabilities
      - Code smells
      - Code coverage
    - Enforce Quality Gate rules.

5. **Containerization Stage**
    - Build Docker image using the Maven artifact.
    - (Optional) Push Docker image to DockerHub, AWS ECR, or GitHub Container Registry.

6. **Deployment**
    - Deploy containerized application to staging/production environments.

---

## Tools Summary

| Tool             | Purpose                                     |
|------------------|---------------------------------------------|
| **Maven**        | Build automation, dependency management     |
| **SonarQube**    | Static code analysis, enforce code quality  |
| **GitHub Actions** | CI/CD pipeline to automate build, scan, and deploy |
| **Docker**       | Containerization of application             |

---

## Example Dockerfile

```dockerfile
FROM openjdk:17-jdk-slim
COPY target/myapp.jar app.jar
ENTRYPOINT ["java", "-jar", "/app.jar"]

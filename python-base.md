# Application Development Lifecycle with Python, SonarQube, GitHub Actions, and Docker

##  Lifecycle Overview

1. **Development Phase**
    - Developers write code (e.g., FastAPI, Django, Flask apps).
    - Local Development:
      ```bash
      python -m venv venv
      source venv/bin/activate
      pip install -r requirements.txt
      pytest  # run unit tests
      ```
      
2. **Version Control (GitHub)**
    - Push code to GitHub.
    - Create Pull Requests (PRs).

3. **CI/CD Automation (GitHub Actions)**
    - Trigger GitHub Actions workflow on `push` or `pull_request`.
    - Steps:
      - Checkout code
      - Set up Python environment
      - Install dependencies
      - Run tests
      - Run SonarQube analysis
      - Build Docker container
      - (Optional) Push Docker container to registry

4. **Quality Assurance (SonarQube)**
    - Analyze code for:
      - Bugs
      - Vulnerabilities
      - Code smells
      - Test coverage
    - Enforce Quality Gate rules.

5. **Containerization Stage**
    - Build Docker image using the Python application.
    - (Optional) Push Docker image to DockerHub, AWS ECR, or GitHub Container Registry.

6. **Deployment**
    - Deploy containerized application to staging/production environments.

---

## Tools Summary

| Tool             | Purpose                                     |
|------------------|---------------------------------------------|
| **Python**       | Application development                    |
| **pytest**       | Unit testing framework                     |
| **SonarQube**    | Static code analysis, enforce code quality  |
| **GitHub Actions** | CI/CD pipeline to automate build, scan, and deploy |
| **Docker**       | Containerization of application             |

---

## Example Dockerfile for Python App

```dockerfile
FROM python:3.11-slim

WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY . .

CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
# application-lifecycle

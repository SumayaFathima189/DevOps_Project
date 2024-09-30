# Java-Jenkins-CI-CD-Pipeline

## Automated CI/CD Pipeline for Java Applications with Jenkins

This repository contains the code and configuration files to set up an automated CI/CD pipeline for a Java-based application using Jenkins. The pipeline is designed to automate the build, test, and deployment processes, ensuring high code quality and security.

## Project Overview
- **Jenkins Pipeline**: Automates the build, test, and deployment process.
- **Tools Integrated**:
  - **SonarQube**: For static code analysis.
  - **Trivy**: For security scanning.
  - **Maven**: For managing Java dependencies and building the application.
  - **Docker**: For containerizing the application.

## Prerequisites

- **Jenkins**: Installed on an EC2 server.
- **SonarQube**: Installed on a separate EC2 server with Docker.
- **Nexus**: Installed on a separate EC2 server with Docker.
- **Trivy**: Installed on the Jenkins server.

## Setup Steps

### Jenkins Setup

1. **Install Jenkins**:
   - Create an EC2 instance for Jenkins.
   - Install Jenkins using the provided script:
     ```bash
     vi jenkins.sh
     chmod +x jenkins.sh
     ./jenkins.sh
     ```

2. **Fork the GitHub Repository**:
   - Fork the repository and add the `gitchecksum` stage to the pipeline.

3. **Install Jenkins Plugins**:
   - Install necessary plugins: `Pipeline`, `Git`, `Maven`, `SonarQube Scanner`, `Docker`, `Eclipse`.

4. **Configure Jenkins Tools**:
   - Add JDK 17, Maven, SonarQube, and Docker in Jenkins' global tool configuration.

5. **Pipeline Script Configuration**:
   - Add stages for `Maven Compile` and `Maven Test` in the pipeline script.

### Trivy Installation

1. **Install Trivy**:
   - Install Trivy on the Jenkins server using the script:
     ```bash
     vi trivy.sh
     chmod +x trivy.sh
     ./trivy.sh
     ```

2. **Add Trivy Stage to the Pipeline**:
   - Include a Trivy stage in the Jenkins pipeline for security scanning.

### SonarQube and Nexus Setup

1. **Create EC2 Instances**:
   - Create EC2 instances for SonarQube and Nexus with at least 30 GB of storage.

2. **Install Docker on EC2 Instances**:
   - Install Docker on all EC2 machines using the script:
     ```bash
     vi docker.sh
     chmod +x docker.sh
     ./docker.sh
     ```

3. **Run Docker Commands**:
   - Run the necessary Docker commands on all EC2 instances to ensure Docker is correctly installed and running.

4. **Set Up SonarQube and Nexus**:
   - Create SonarQube and Nexus containers using Docker on their respective servers.
   - Access them via the public IP:
     - SonarQube: `http://<public-ip>:9000`
     - Nexus: `http://<public-ip>:8081`

5. **SonarQube Configuration**:
   - Create a SonarQube token for Jenkins and add it in Jenkins credentials.
   - Set up SonarQube webhook URL in Jenkins.

6. **Nexus Configuration**:
   - Configure Nexus repository URLs in the `pom.xml` file.
   - Add Nexus server details in Jenkins' global Maven settings.

### Pipeline Stages

1. **Maven Build and Test**:
   - Add stages in the pipeline for Maven compile and test.

2. **SonarQube Analysis**:
   - Add a stage for SonarQube static code analysis.

3. **Trivy Security Scanning**:
   - Add a Trivy stage to scan Docker images.

4. **Docker Build and Deploy**:
   - Add stages to build and tag Docker images.
   - Push images to Docker Hub.

5. **Nexus Deployment**:
   - Add a stage to deploy artifacts to Nexus repositories.

## Final Steps

- **Docker Permissions**: Ensure Docker permissions are correctly set on the Jenkins server.
  ```bash
  sudo chmod 666 /var/run/docker.sock

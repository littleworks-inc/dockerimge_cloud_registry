# AWS Build and Publish Docker Image

This GitHub Actions pipeline automates the build and push of a Docker image to AWS ECR (Elastic Container Registry). It triggers on every push to any branch.

## Workflow Overview

- **Checkout:** Fetches the repository's code.
- **Set up QEMU:** Sets up QEMU for emulation if needed.
- **Set up Docker Buildx:** Sets up Docker Buildx for building multi-platform images.
- **Lint Action for AWS:** Checks Dockerfile for best practices using Hadolint.
- **Cache Docker layers:** Caches Docker layers to improve build performance.
- **Configure AWS Credentials:** Configures AWS credentials for pushing to ECR.
- **Login to Amazon ECR:** Logs in to Amazon ECR using AWS credentials.
- **Set Short SHA:** Retrieves the short SHA of the latest commit.
- **Build and Push:** Builds the Docker image and pushes it to AWS ECR.
- **Run Trivy Vulnerability Scanner:** Scans the Docker image for vulnerabilities using Trivy.

## Pipeline Details

- **Environment Variables:**
  - `REGISTRY`: AWS ECR registry URL.
  - `IMAGE_NAME`: Name of the Docker image.
  - `COMPARE_TAG`: Tag to compare for changes.
  - `SHA`: SHA of the latest commit.

- **Prerequisites:**
  - AWS credentials stored as secrets in the repository (`AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`, `AWS_DEFAULT_REGION`).
  - Dockerfile located in `aws/` directory.

- **Output:**
  - Docker image pushed to AWS ECR.
  - Trivy vulnerability scan results.

## Usage

1. Ensure AWS credentials are added as secrets in the repository.
2. Create or update the Dockerfile in the `aws/` directory.
3. Make changes and push to trigger the pipeline.

For more information about AWS ECR, Docker Buildx, and Trivy, refer to the official documentation.


# Building and Publishing a Docker Image with Google Cloud Platform (GCP) on GitHub Actions

This GitHub Actions pipeline automates the process of building and publishing a Docker image to Google Cloud Platform's Container Registry (GCR). It ensures that the Docker image is built securely and scanned for vulnerabilities before pushing it to the registry. Let's break down the steps involved:

## Step 1: Checkout

This step checks out the source code of your project.

## Step 2: Debug

Prints out the GitHub reference for debugging purposes.

## Step 3: Lint Action for GCP

Uses Hadolint to lint the Dockerfile, ensuring best practices and identifying potential issues. The linting process will only throw warnings and won't fail the pipeline.

## Step 4: Authenticate with Google Cloud Platform

This step authenticates with GCP using the provided service account credentials stored in GitHub secrets.

## Step 5: Set up Cloud SDK

Sets up the Google Cloud SDK for further interactions with GCP services.

## Step 6: Use gcloud CLI

Verifies the setup by printing out information about the configured gcloud CLI.

## Step 7: Docker Authentication

Configures Docker to authenticate with GCR using the gcloud CLI.

## Step 8: Build Docker Image

Builds the Docker image using the specified Dockerfile and tags it with the GCR repository path.

## Step 9: Push Docker Image

Pushes the built Docker image to the Google Container Registry.

## Step 10: Run Trivy Vulnerability Scanner

Scans the Docker image for vulnerabilities using Trivy. The results are displayed in a table format and the pipeline continues even if vulnerabilities are found.

---

### Prerequisites

- Google Cloud Platform project with Container Registry enabled.
- Service account key JSON file stored securely as a GitHub secret.
- Dockerfile located in the `gcp` directory of your repository.
- Trivy vulnerability scanner action setup (if not already done).

### Usage

1. Ensure your Dockerfile is located in the `gcp` directory.
2. Store your Google Cloud service account key JSON file securely as a GitHub secret named `GOOGLE_CREDENTIALS`.
3. Customize environment variables like `PROJECT_ID`, `REGESTRY_name`, `REGION`, and `IMAGE_NAME` according to your GCP setup.
4. Commit and push your changes to trigger the pipeline.

By following this pipeline, you can automate the process of building and publishing Docker images to Google Cloud Platform securely and efficiently.

# Azure Build and Publish Docker Image Pipeline

This GitHub Actions pipeline automates the build and publishing of a Docker image to Azure Container Registry. The pipeline includes linting for Dockerfiles, Docker image scanning for vulnerabilities using Trivy, and pushing the built Docker image to Azure Container Registry.

## Pipeline Overview

The pipeline consists of the following steps:

1. **Checkout**: This step checks out the source code of the repository.

2. **Lint Action for Azure**: Uses Hadolint to lint the Dockerfile located in the `azure/` directory, ensuring adherence to best practices and standards.

3. **Azure Credentials**: Logs into Azure Container Registry using the provided Azure credentials stored as GitHub repository secrets.

4. **Build Docker Image**: Builds the Docker image using the Dockerfile located in the `azure/` directory.

5. **Push Docker Image**: Pushes the built Docker image to Azure Container Registry.

6. **Run Trivy Vulnerability Scanner**: Scans the pushed Docker image for vulnerabilities using Trivy, reporting any identified vulnerabilities.

## Usage

To use this pipeline in your repository, follow these steps:

1. Ensure that you have the necessary Azure credentials (AZURE_CLIENT_ID, ARM_CLIENT_SECRET) added as GitHub repository secrets.

2. Place your Dockerfile for the Azure application in the `azure/` directory of your repository.

3. Customize the `IMAGE_NAME` and `container_registry` environment variables in the pipeline YAML file according to your project requirements.

4. Commit the pipeline YAML file (azure-pipeline.yml) to your repository.

5. Upon pushing changes to the repository, the pipeline will be triggered automatically, building and pushing the Docker image to Azure Container Registry.

## Notes

- Ensure that the Dockerfile in the `azure/` directory is properly configured to include all necessary dependencies and configurations for your Azure application.

- Regularly review the pipeline and update the versions of actions and tools used to benefit from bug fixes and new features.

- Test the pipeline in a staging environment before deploying to production to ensure proper functionality and adherence to security standards.

## Resources

- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [Azure Container Registry Documentation](https://docs.microsoft.com/en-us/azure/container-registry/)
- [Hadolint Documentation](https://github.com/hadolint/hadolint)
- [Trivy Documentation](https://github.com/aquasecurity/trivy)


## GitHub Actions Pipeline for Docker Image Deployment with CoGuard Integration

This GitHub Actions pipeline automates the build, linting, and deployment process for a Docker image named `gcpcli` to Google Cloud Platform's Container Registry. The pipeline also integrates CoGuard.io for scanning the Docker image for vulnerabilities.

### Pipeline Structure

The pipeline consists of the following stages:

1. **Checkout**: Fetches the repository code.
2. **Debug**: Prints the GitHub reference.
3. **Linting**: Uses Hadolint to lint the Dockerfile.
4. **Authentication**: Authenticates with Google Cloud.
5. **Cloud SDK Setup**: Sets up the Google Cloud SDK.
6. **Docker Authentication**: Configures Docker authentication for Google Container Registry.
7. **Build Docker Image**: Builds the Docker image using the specified Dockerfile.
8. **Push Docker Image**: Pushes the built Docker image to Google Container Registry.
9. **CoGuard Scan**: Scans the Docker image for vulnerabilities using CoGuard.io.

### CoGuard CLI Action Explanation

The `CoGuard Scan` step in the pipeline utilizes the `coguardio/coguard-scan-action@v0.2.2` GitHub Action to scan the Docker image for vulnerabilities using CoGuard.io. CoGuard is a static analysis tool for configuration files that helps developers and infrastructure teams reduce false positives and find actionable fixes for cloud infrastructure and application configurations before and after provisioning.

#### CoGuard's Features

- **IaC, Container, and Application Configuration Scanning**: CoGuard scans configuration files in your code repository, including Terraform, Kubernetes YAML, Dockerfile, and other configuration files. It also connects to your cloud provider and extracts your configurations.
  
- **Automating Compliance**: CoGuard can be added to your CI/CD pipeline, allowing for continual compliance testing and monitoring. It supports a wide range of compliance frameworks and can provide ongoing reporting.
  
- **Remediation with or without Automation**: CoGuard provides auto-remediation tools that can create a pull-request and fit in the code review process. It also provides manual remediation steps for configuration switches across containers and applications.
  
- **Reduce CVE False Positives**: CoGuard is built to focus on actionable configuration changes, not CVE noise. It uses a predicate logic engine to add new technologies or new rulesets that are independent of the configuration of environments.
  
- **Fast and Extensible**: CoGuard is built from the ground up to be extensible, and its predicate logic engine allows teams to extend the policies and configuration rules supported quickly.
  
- **Supported Technologies**: CoGuard supports a wide range of technologies, including public cloud providers, infrastructure as code (IaC), and containerization technologies. It also supports databases, serverless technologies, and more.
  
- **Dashboard and Reporting**: CoGuard provides a dashboard that displays all reports, including history and trends. It also provides remediation steps and allows teams to view their full infrastructure and access additional features.

CoGuard offers a free Developer Tier that supports common IaC and AMP technology stacks. It also offers a paid tier with additional features, including auto-remediation and access to the full infrastructure.

By integrating CoGuard.io into the pipeline, the company ensures that the Docker images deployed to production are secure and free from known vulnerabilities, enhancing the overall security posture of the applications running in the containerized environment.

### Usage

To use this pipeline, follow these steps:

1. Ensure you have the necessary secrets set up in your GitHub repository:
    - `GOOGLE_CREDENTIALS`: Google Cloud service account credentials.
    - `CoGuardUserName`: CoGuard username for authentication.
    - `CoGuardPassword`: CoGuard password for authentication.

2. Modify the pipeline code in `.github/workflows/main.yml` to suit your specific requirements, such as changing the Docker image name, Google Cloud project ID, or other environment variables.

3. Push your changes to the repository. The GitHub Actions pipeline will be triggered automatically on push events to build, lint, and deploy the Docker image, as well as scan it for vulnerabilities using CoGuard.io.

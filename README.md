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


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
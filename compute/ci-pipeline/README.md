# Lab: Set Up GitHub Actions Pipeline for Spring Boot Application with Azure Container Registry (ACR)

## Overview
In this lab, you will:
1. Write a build script for GitHub Actions to build a Docker image for your Spring Boot application.
2. Publish the Docker image to Azure Container Registry (ACR).
3. Set up OpenID Connect (OIDC) authentication to allow GitHub Actions to push the Docker image to ACR without storing Azure credentials in GitHub secrets.

## Prerequisites
- An **Azure Subscription** with permission to create resources.
- An **Azure Container Registry (ACR)** instance.
- A **GitHub Repository** containing your Spring Boot application code and Dockerfile.
- **Dockerfile** in the root directory of your repository.

---

## Steps

### Step 1: Set Up Azure Container Registry (ACR)

1. **Create Azure Container Registry**
   - In the **Azure Portal**, search for **Container Registry** and select **Create**.
   - Select your **Subscription** and create or choose an existing **Resource Group**.
   - Enter a unique **Registry Name** (e.g., `myspringappregistry`).
   - Select the **SKU** (e.g., Basic).
   - Click **Review + Create**, then **Create**.

2. **Note the Login Server URL**
   - After creation, go to the ACR's **Overview** page.
   - Note the **Login server** URL (e.g., `myspringappregistry.azurecr.io`), which you’ll use as the registry URL in the GitHub Actions workflow.

---

### Step 2: Set Up Azure Entra ID (Azure AD) for OIDC Authentication

1. **Register an Application in Azure Entra ID**
   - In **Azure Portal**, navigate to **Azure Active Directory** > **App registrations**.
   - Select **+ New registration**.
   - Name the app (e.g., `GitHub-OIDC-SpringApp`).
   - Under **Supported account types**, select **Single tenant**.
   - Click **Register**.

2. **Create a Federated Credential**
   - Go to **Certificates & secrets** in the app registration and select **Federated credentials**.
   - Click **+ Add credential** and choose **GitHub Actions** as the scenario.
   - Configure the credential:
     - **Organization**: Your GitHub organization or username.
     - **Repository**: The GitHub repository (e.g., `username/repo-name`).
     - **Branch**: The branch that will use OIDC (e.g., `main`).
   - Click **Add** to create the federated credential.

3. **Assign Permissions for ACR**
   - Go to your **Azure Container Registry**.
   - Under **Access control (IAM)**, select **+ Add role assignment**.
   - Assign the **AcrPush** role to the app registration created in Step 2 (e.g., `GitHub-OIDC-SpringApp`).
   - This will allow GitHub Actions to push Docker images to ACR.

---

### Step 3: Write GitHub Actions Workflow to Build and Push Docker Image

Create a new GitHub Actions workflow file in your GitHub repository at `.github/workflows/build-and-push.yml`.

#### `.github/workflows/build-and-push.yml`

```yaml
name: Build and Push Docker Image to ACR

on:
  push:
    branches:
      - main

permissions:
  id-token: write
  contents: read

jobs:
  build-and-push:
    runs-on: ubuntu-latest

    steps:
      # Step 1: Checkout code
      - name: Checkout code
        uses: actions/checkout@v2

      # Step 2: Log in to Azure CLI with OpenID Connect (OIDC)
      - name: Log in to Azure CLI
        uses: azure/login@v1
        with:
          client-id: ${{ secrets.AZURE_CLIENT_ID }}
          tenant-id: ${{ secrets.AZURE_TENANT_ID }}
          subscription-id: ${{ secrets.AZURE_SUBSCRIPTION_ID }}
          enable-AzPSSession: true

      # Step 3: Build Docker Image
      - name: Build Docker image
        run: |
          docker build -t my-spring-app:latest .

      # Step 4: Tag Docker Image with ACR URL
      - name: Tag Docker image
        run: |
          docker tag my-spring-app:latest myspringappregistry.azurecr.io/my-spring-app:latest

      # Step 5: Push Docker Image to ACR
      - name: Push Docker image to ACR
        run: |
          docker push myspringappregistry.azurecr.io/my-spring-app:latest

```

### Step 4: Add Secrets to GitHub Repository

1. In your GitHub repository, navigate to **Settings > Secrets and variables > Actions**.

2. Click **New repository secret** to add each of the following secrets:

   - **AZURE_CLIENT_ID**: Enter the **Client ID** of the app registration created in **Step 2**.
   - **AZURE_TENANT_ID**: Enter your **Azure AD Tenant ID**.
   - **AZURE_SUBSCRIPTION_ID**: Enter your **Azure Subscription ID**.

These secrets are securely stored in GitHub and will be referenced in the GitHub Actions workflow to authenticate and authorize access to Azure.

---

### Step 5: Test the GitHub Actions Workflow

1. **Commit the Workflow File**

   - Push the `.github/workflows/build-and-push.yml` file to the **main** branch of your GitHub repository.

2. **Monitor the Workflow Execution**

   - In your GitHub repository, go to the **Actions** tab.
   - Select the **Build and Push Docker Image to ACR** workflow to view the logs and monitor the execution of each step.

3. **Verify the Docker Image in ACR**

   - In the **Azure Portal**, go to **Azure Container Registry** and navigate to **Repositories**.
   - Confirm that your Docker image (e.g., `my-spring-app`) was successfully pushed to ACR.

---

### Summary
In this lab, you:

- Set up Azure Container Registry (ACR).
- Configured Azure Entra ID (Azure AD) to allow GitHub Actions to authenticate via OpenID Connect (OIDC).
- Created a GitHub Actions workflow to build and push a Docker image to ACR securely.
- Verified the successful deployment of your Docker image to ACR.

This lab demonstrates a secure and streamlined way to manage Docker images for a Spring Boot application, using GitHub Actions and ACR with modern OIDC authentication.

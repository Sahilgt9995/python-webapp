# Task 2: CI/CD Pipeline Implementation (GitHub Actions)

## Overview
This task involves setting up a **CI/CD pipeline** using **GitHub Actions** to automate the deployment of the Python web application to **Azure App Service**.

## CI/CD Pipeline Configuration
The pipeline is defined in the `main_myapp123.yml` file located in `.github/workflows/`.

### **GitHub Actions Workflow (`main_myapp123.yml.yml`)**
```yaml
name: Deploy to Azure Web App

on:
  push:
    branches:
      - main 

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Repository
        uses: actions/checkout@v4

      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.9'

      - name: Install Dependencies
        run: |
          pip install -r requirements.txt

      - name: Deploy to Azure Web App
        uses: azure/webapps-deploy@v2
        with:
          app-name: "myapp123"  
          publish-profile: ${{ secrets.AZURE_WEBAPP_PUBLISH_PROFILE }}
          package: .
```

## **Pipeline Stages Explained**
1. **Checkout Repository** → Clones the GitHub repository to the runner machine.
2. **Set up Python** → Installs Python 3.9 on the GitHub Actions runner.
3. **Install Dependencies** → Installs required Python libraries from `requirements.txt`.
4. **Deploy to Azure** → Uses the `azure/webapps-deploy@v2` action to deploy the application to Azure App Service.

## **Secrets Management**
- **`AZURE_WEBAPP_PUBLISH_PROFILE`** → Stored in GitHub Secrets for **secure authentication**.
- This secret is obtained from Azure App Service and is used to authenticate the deployment.

## **How to Trigger Deployment**
- Every time a commit is pushed to the `main` branch, the **GitHub Actions workflow** is triggered automatically.
- You can check the deployment status under the **Actions tab** in GitHub.



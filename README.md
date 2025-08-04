# GitHub Actions CI/CD Pipeline

This directory contains the GitHub Actions workflows for the FinTrack project CI/CD pipeline.

## Workflows

### 1. `backend-tests.yml`
- **Purpose**: Runs backend (Spring Boot) tests
- **Trigger**: Push and Pull Requests
- **Features**:
  - Java 17 setup with Temurin distribution
  - Maven dependency caching
  - Test execution with `./mvnw test`
  - Code coverage upload to Codecov

### 2. `frontend-tests.yml`
- **Purpose**: Runs frontend (React) tests and build
- **Trigger**: Push and Pull Requests
- **Features**:
  - Node.js 18 setup with npm caching
  - Dependency installation with `npm ci`
  - Test execution with Jest
  - Production build verification
  - Code coverage upload to Codecov

### 3. `etl-tests.yml`
- **Purpose**: Runs ETL (Python) tests
- **Trigger**: Push and Pull Requests
- **Features**:
  - Python 3.11 setup
  - pip dependency caching
  - Test execution with pytest
  - Coverage reporting (XML and HTML)
  - Code coverage upload to Codecov

### 4. `deployment.yml`
- **Purpose**: Deploys to AWS infrastructure
- **Trigger**: Push to main branch or manual dispatch
- **Features**:
  - AWS credentials configuration
  - ECR login and Docker image push
  - S3 frontend deployment
  - CloudFront cache invalidation
  - ECS service deployment

### 5. `all-tests.yml`
- **Purpose**: Runs all tests in parallel
- **Trigger**: Push and Pull Requests
- **Features**:
  - Parallel execution of backend, frontend, and ETL tests
  - Consolidated coverage reporting
  - Faster feedback for developers

## Required Secrets

For the deployment workflow to work, you need to configure these secrets in your GitHub repository:

### AWS Credentials
- `AWS_ACCESS_KEY_ID`: AWS access key
- `AWS_SECRET_ACCESS_KEY`: AWS secret key
- `AWS_REGION`: AWS region (e.g., us-east-1)

### AWS Resources
- `S3_BUCKET`: S3 bucket name for frontend deployment
- `CLOUDFRONT_DISTRIBUTION_ID`: CloudFront distribution ID
- `ECS_CLUSTER`: ECS cluster name
- `ECS_SERVICE`: ECS service name

## Setup Instructions

1. **Enable GitHub Actions**: Go to your repository Settings > Actions > General and enable Actions

2. **Configure Secrets**: Go to Settings > Secrets and variables > Actions and add the required secrets

3. **Push to Trigger**: Push to any branch to trigger the test workflows, or push to main to trigger deployment

## Coverage Thresholds

The workflows are configured to upload coverage reports to Codecov with these targets:
- **Backend**: 80% minimum
- **Frontend**: 70% minimum  
- **ETL**: 75% minimum

## Local Testing

Before pushing, you can test the workflows locally:

```bash
# Backend
cd financial-tracker-backend
./mvnw test

# Frontend
cd financial-tracker-frontend
npm ci
npm test -- --watchAll=false --passWithNoTests
npm run build

# ETL
cd financial-tracker-etl
pip install -r requirements.txt
python -m pytest tests/ -v
```

## Troubleshooting

### Common Issues

1. **Maven Wrapper Missing**: Ensure `mvnw` and `mvnw.cmd` exist in the backend directory
2. **Node Modules**: Frontend workflow uses `npm ci` for clean installs
3. **Python Dependencies**: ETL workflow installs from `requirements.txt`
4. **AWS Permissions**: Ensure the AWS credentials have proper IAM permissions

### Debugging

- Check the Actions tab in your GitHub repository for detailed logs
- Use `workflow_dispatch` trigger for manual testing
- Review the "Run Tests" step logs for specific error messages 
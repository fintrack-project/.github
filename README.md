# FinTrack CI/CD Testing Pipeline

This directory contains GitHub Actions testing workflows and documentation for the FinTrack project.

## Repository Structure

The testing workflows are distributed across individual repositories:

```
fintrack-project/
├── financial-tracker-frontend/
│   └── .github/workflows/
│       └── frontend-tests.yml          ✅ Frontend CI pipeline
├── financial-tracker-backend/
│   └── .github/workflows/
│       └── backend-tests.yml           ✅ Backend CI pipeline
├── financial-tracker-etl/
│   └── .github/workflows/
│       └── etl-tests.yml               ✅ ETL CI pipeline
└── financial-tracker-infra/
    └── .github/workflows/
        └── (No GitHub Actions deployment)
    └── ci-cd/
        └── Jenkinsfile                    ✅ Jenkins CI/CD Pipeline
```

## Testing Workflow Details

### 1. Frontend Tests (`financial-tracker-frontend/.github/workflows/frontend-tests.yml`)
- **Purpose**: Runs frontend (React) tests and build
- **Trigger**: Push and Pull Requests
- **Features**:
  - Node.js 18 setup with npm caching
  - Dependency installation with `npm ci`
  - Test execution with Jest (`--watchAll=false --passWithNoTests`)
  - Production build verification
  - Code coverage upload to Codecov

### 2. Backend Tests (`financial-tracker-backend/.github/workflows/backend-tests.yml`)
- **Purpose**: Runs backend (Spring Boot) tests
- **Trigger**: Push and Pull Requests
- **Features**:
  - Java 21 setup with Temurin distribution
  - Maven dependency caching
  - Test execution with `./mvnw test`
  - Code coverage upload to Codecov

### 3. ETL Tests (`financial-tracker-etl/.github/workflows/etl-tests.yml`)
- **Purpose**: Runs ETL (Python) tests
- **Trigger**: Push and Pull Requests
- **Features**:
  - Python 3.11 setup
  - pip dependency caching
  - Test execution with pytest
  - Coverage reporting (XML and HTML)
  - Code coverage upload to Codecov

### 4. Jenkins CI/CD Pipeline (`financial-tracker-infra/ci-cd/Jenkinsfile`)
- **Purpose**: Build and deploy Docker images to Quay.io registry
- **Status**: ✅ Fully implemented and working
- **Features**:
  - Multi-service Docker image building (Frontend, Backend, ETL)
  - Environment-specific builds (dev/prod)
  - Container registry integration (Quay.io)
  - Automated versioning and tagging
  - Health checks and validation

## Required Secrets

For the test workflows to work, you need to configure these secrets in each repository:

### Codecov Integration
- `CODECOV_TOKEN`: Codecov token for coverage reporting

### Jenkins CI/CD Pipeline
- **Container Registry**: Quay.io integration with automated image pushing
- **Build Environments**: Development and production builds with versioning
- **Service Orchestration**: Multi-service Docker image building and deployment
- **Automation**: Jenkins pipeline with parameterized builds and validation

## Setup Instructions

1. **Enable GitHub Actions**: Go to each repository Settings > Actions > General and enable Actions

2. **Configure Secrets**: Go to each repository Settings > Secrets and variables > Actions and add the required secrets

3. **Create Pull Requests**: Each repository has a `178-cicd-pipeline` branch with the workflows ready for PR

4. **Push to Trigger**: Push to any branch to trigger the test workflows

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
python -m pytest tests/ -v --cov=etl
```

## Jenkins CI/CD Pipeline Details

The Jenkins pipeline in `financial-tracker-infra/ci-cd/` provides comprehensive CI/CD capabilities:

### **Pipeline Features**
- **Multi-Service Building**: Frontend, Backend, and ETL services
- **Environment Management**: Development and production builds
- **Version Control**: Automated versioning with semantic versioning
- **Container Registry**: Quay.io integration for image storage
- **Health Checks**: Service validation and monitoring
- **Parameterized Builds**: Flexible build configuration

### **Build Process**
1. **Environment Validation**: Checks branch permissions and required files
2. **Service Building**: Clones repositories and builds Docker images
3. **Image Tagging**: Applies version tags and environment labels
4. **Registry Push**: Uploads images to Quay.io container registry
5. **Cleanup**: Removes temporary files and Docker artifacts

## Repository URLs

- **Frontend**: https://github.com/fintrack-project/financial-tracker-frontend
- **Backend**: https://github.com/fintrack-project/financial-tracker-backend
- **ETL**: https://github.com/fintrack-project/financial-tracker-etl
- **Infra**: https://github.com/fintrack-project/financial-tracker-infra

## Troubleshooting

### Common Issues

1. **Maven Wrapper Missing**: Ensure `mvnw` and `mvnw.cmd` exist in the backend directory
2. **Node Modules**: Frontend workflow uses `npm ci` for clean installs
3. **Python Dependencies**: ETL workflow installs from `requirements.txt`
4. **Docker Permissions**: Ensure Docker has proper permissions for local development

### Debugging

- Check the Actions tab in each GitHub repository for detailed logs
- Use `workflow_dispatch` trigger for manual testing
- Review the "Run Tests" step logs for specific error messages

## Project Status

- ✅ **Test Workflows**: Each repository has its own CI pipeline for testing
- ✅ **Jenkins CI/CD**: Full Docker image building and deployment pipeline
- ✅ **Container Registry**: Quay.io integration with automated image management
- ✅ **Local Development**: Docker Compose for local development and testing
- ✅ **Code Quality**: Automated testing, coverage reporting, and deployment 
# GitHub Actions CI/CD Pipeline

This directory contains shared GitHub Actions configurations and documentation for the FinTrack project.

## Repository Structure

The CI/CD workflows are now properly distributed across individual repositories:

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
        └── deployment.yml               ✅ AWS deployment pipeline
```

## Workflow Details

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

### 4. Deployment (Not Yet Implemented)
- **Purpose**: Will deploy to containerized infrastructure
- **Status**: Planning phase
- **Planned Features**:
  - Docker image building and pushing
  - Container orchestration deployment
  - Health checks and monitoring
  - Automated rollback capabilities

## Required Secrets

For the test workflows to work, you need to configure these secrets in each repository:

### Codecov Integration
- `CODECOV_TOKEN`: Codecov token for coverage reporting

### Future Deployment (When Implemented)
- Container registry credentials
- Deployment environment variables
- Health check endpoints

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
4. **Docker Permissions**: Ensure Docker has proper permissions for building images

### Debugging

- Check the Actions tab in each GitHub repository for detailed logs
- Use `workflow_dispatch` trigger for manual testing
- Review the "Run Tests" step logs for specific error messages

## Migration Notes

- ✅ Workflows moved from centralized `.github` repository to individual repositories
- ✅ Each repository now has its own CI/CD pipeline
- ✅ Workflows will trigger when code is pushed to their respective repositories
- ✅ Deployment workflow is in the infrastructure repository for centralized deployment management 
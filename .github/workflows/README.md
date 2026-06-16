# CI/CD Pipelines Documentation

This directory contains GitHub Actions workflows for automated CI/CD pipelines across multiple projects in this DevOps learning repository.

## 📋 Overview

| Workflow | Project | Purpose | Triggers |
|----------|---------|---------|----------|
| `python-ci.yml` | ci_pipeline-main | Python testing, linting, security | Push/PR to main/master |
| `nodejs-docker-ci.yml` | Nodeapp-main | Node.js build, Docker build & push | Push/PR to main/master |
| `bash-validation-ci.yml` | Day_1-in-DevOps-main | Bash script validation & testing | Push/PR to main/master |
| `week3-docker-ci.yml` | Week_3-main | Python app with Docker build & push | Push/PR to main/master |

## 🚀 Features

### All Pipelines Include:
- ✅ **Automated Testing** - Runs on every push and pull request
- ✅ **Path-based Triggers** - Only runs when relevant files change
- ✅ **Code Quality Checks** - Linting and syntax validation
- ✅ **Security Scanning** - Bandit for Python, Docker Scout for containers
- ✅ **Docker Layer Caching** - Faster builds with cached layers
- ✅ **Build Reports** - Automatic summaries in GitHub Actions tab
- ✅ **Conditional Deployment** - Only pushes to Docker Hub on main branch

### Python CI Pipeline (`python-ci.yml`)
- Python 3.12 with pip caching
- Pytest with coverage reporting
- Flake8 code linting
- Bandit security scanning
- Coverage report artifact upload

### Node.js Docker Pipeline (`nodejs-docker-ci.yml`)
- Node.js 20 with npm caching
- Docker Buildx for efficient builds
- Docker Scout vulnerability scanning
- Container health checks
- Docker Hub push with version tags
- Build metadata (BUILD_DATE, VCS_REF)

### Bash Validation Pipeline (`bash-validation-ci.yml`)
- Syntax validation for all .sh scripts
- ShellCheck static analysis
- Executable permission checks
- Dry-run testing for backup scripts
- Comprehensive validation reporting

### Week 3 Docker Pipeline (`week3-docker-ci.yml`)
- Python 3.10 runtime
- Code quality and security checks
- Docker image building with metadata
- Vulnerability scanning
- Docker Hub integration

## 🔐 Required Secrets

For Docker Hub push functionality, configure these repository secrets:

1. Go to your GitHub repository → Settings → Secrets and variables → Actions
2. Add the following secrets:

| Secret Name | Description | Example |
|-------------|-------------|---------|
| `DOCKERHUB_USERNAME` | Your Docker Hub username | `yourusername` |
| `DOCKERHUB_TOKEN` | Docker Hub access token | `dckr_pat_xxxxxxxxxxxx` |

### How to Create Docker Hub Token:
1. Login to https://hub.docker.com
2. Go to Account Settings → Security
3. Click "New Access Token"
4. Give it a name and select Read & Write permissions
5. Copy the token and add it to GitHub secrets

## 📊 Viewing Pipeline Results

1. Navigate to the **Actions** tab in your GitHub repository
2. Select any workflow run to see detailed logs
3. Check the **Summary** section for build reports
4. Download artifacts (like coverage reports) from successful runs

## 🎯 Learning Objectives

These pipelines demonstrate key DevOps concepts:

- **Continuous Integration** - Automated testing on every change
- **Infrastructure as Code** - Version-controlled pipeline definitions
- **Containerization** - Docker image building and management
- **Security** - Automated vulnerability scanning
- **Quality Assurance** - Code linting and testing
- **Artifact Management** - Docker registry integration
- **Observability** - Build reports and status tracking

## 🛠️ Customization

### Modify Trigger Paths
Edit the `paths:` section in each workflow to change which file changes trigger the pipeline.

### Add More Tests
- Python: Add more test files in `ci_pipeline-main/`
- Node.js: Add Jest/Mocha tests in `Nodeapp-main/`
- Bash: Add more validation scripts in `Day_1-in-DevOps-main/`

### Enable Notifications
Add Slack/Discord/Email notifications by adding steps like:

```yaml
- name: Notify on failure
  if: failure()
  uses: slackapi/slack-github-action@v1
  with:
    payload: |
      {
        "text": "Pipeline failed: ${{ github.workflow }}"
      }
  env:
    SLACK_WEBHOOK_URL: ${{ secrets.SLACK_WEBHOOK }}
```

## 📚 Best Practices Demonstrated

1. **Pin Action Versions** - Using specific versions (e.g., `@v4`) for reproducibility
2. **Job Dependencies** - Using `needs:` to ensure proper execution order
3. **Conditional Execution** - Using `if:` for environment-specific steps
4. **Caching** - Speeding up builds with dependency and layer caching
5. **Error Handling** - Using `|| echo` for non-critical steps
6. **Build Metadata** - Adding timestamps and commit references to images
7. **Security Scanning** - Integrating vulnerability checks in the pipeline

## 🔍 Troubleshooting

### Pipeline Not Triggering?
- Check that you're pushing to `main` or `master` branch
- Verify file paths match the `paths:` filter
- Ensure workflow files are in `.github/workflows/`

### Docker Push Failing?
- Verify Docker Hub secrets are configured correctly
- Check that the token has write permissions
- Ensure image names don't conflict

### Tests Failing?
- Review the job logs for specific error messages
- Run tests locally to reproduce issues
- Check dependencies are installed correctly

## 📖 Additional Resources

- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [Docker Buildx](https://github.com/docker/buildx)
- [ShellCheck](https://www.shellcheck.net/)
- [Pytest](https://docs.pytest.org/)
- [Bandit](https://bandit.readthedocs.io/)

---

**Happy Learning! 🚀**

*These pipelines are designed for educational purposes to help you learn DevOps practices hands-on.*

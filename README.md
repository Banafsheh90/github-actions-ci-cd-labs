# GitHub Actions CI/CD Labs

This repository contains hands-on CI/CD workflow implementations using GitHub Actions. It is organized as a collection of focused labs for building, testing, debugging, packaging, and improving automated workflows across different project types.

The goal is to practice clean workflow configuration, automated testing, dependency management, matrix builds, reusable workflows, container image delivery, and CI/CD debugging in a reproducible repository structure.

Each lab is kept in its own folder, while GitHub Actions workflow files are stored in `.github/workflows/`.

## Labs

| Lab | Focus | Status |
|---|---|---|
| [Django CI Workflow](challenge-01-django-ci/) | Django test automation, Python matrix builds, dependency installation, workflow debugging | Completed |
| [Container Image Delivery](challenge-02-container-image/) | Reusable Python integration workflow, Docker image build, GitHub Packages publishing, and container image signing | Completed |

More labs will be added as the repository expands.

## Workflows

* `.github/workflows/django-ci.yml`  
  Runs the Django CI workflow and tests the project across multiple Python versions.

* `.github/workflows/02-container-python-ci.yml`  
  Defines a reusable Python integration workflow that installs dependencies, runs linting, executes tests, and publishes a test report.

* `.github/workflows/02-container-publish.yml`  
  Runs the container delivery pipeline. It calls the reusable integration workflow first, then builds, publishes, and signs a Docker image using GitHub Packages.

## Key Concepts Practiced

- GitHub Actions workflow structure
- CI triggers for push and pull request events
- GitHub-hosted runners
- Repository checkout inside a runner
- Python setup in CI
- Dependency installation from `requirements.txt`
- Matrix testing across multiple Python versions
- Reading workflow logs to debug failed jobs
- Fixing missing dependencies in a reproducible way
- Reusable workflows with `workflow_call`
- Workflow dependencies with `needs`
- Job-level permissions
- Docker image build and publish workflows
- GitHub Container Registry publishing
- Container image signing with cosign
- Keeping lab projects in subfolders while workflows live in `.github/workflows/`

## Repository Structure

```text
github-actions-ci-cd-labs/
├── .github/
│   └── workflows/
│       ├── django-ci.yml
│       ├── 02-container-python-ci.yml
│       └── 02-container-publish.yml
├── challenge-01-django-ci/
├── challenge-02-container-image/
└── README.md
```

## Notes

This repository is focused on practical CI/CD workflow implementation. Each lab is structured to highlight a specific GitHub Actions concept clearly and keep the workflow setup easy to review.

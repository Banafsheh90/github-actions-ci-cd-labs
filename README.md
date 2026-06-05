# GitHub Actions CI/CD Labs

This repository contains hands-on CI/CD workflow implementations using GitHub Actions. It is organized as a collection of focused labs for building, testing, debugging, and improving automated workflows across different project types.

The goal is to practice clean workflow configuration, automated testing, dependency management, matrix builds, and CI debugging in a reproducible repository structure.

Each lab is kept in its own folder, while GitHub Actions workflow files are stored in `.github/workflows/`.

## Labs

| Lab | Focus | Status |
|---|---|---|
| [Django CI Workflow](challenge-01-django-ci/) | Django test automation, Python matrix builds, dependency installation, workflow debugging | Completed |

More labs will be added as the repository expands.

## Workflows

| Workflow | Related Lab | Description |
|---|---|---|
| `.github/workflows/django-ci.yml` | Django CI Workflow | Runs Django tests across multiple Python versions using GitHub Actions |

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

## Notes

This repository is focused on practical CI/CD workflow implementation. Each lab is structured to highlight a specific GitHub Actions concept clearly and keep the workflow setup easy to review.
# 02 Container Image Delivery

This lab implements a continuous delivery workflow for a Python application using GitHub Actions and GitHub Packages.

The pipeline first runs a reusable Python integration workflow. If the integration job succeeds, a delivery workflow builds a Docker image, publishes it to GitHub Container Registry, and signs the published image with cosign.

## Application

The sample application is a small Python service with tests and a Dockerfile.

Key files:

```text
challenge-02-container-image/
├── Dockerfile
├── main.py
├── main_test.py
├── requirements.txt
├── pyproject.toml
├── config.py
├── data.json
└── README.md
```

## Workflows

This lab uses two GitHub Actions workflows stored at the repository root.

```text
.github/workflows/02-container-python-ci.yml
.github/workflows/02-container-publish.yml
```

### Reusable integration workflow

`02-container-python-ci.yml` defines a reusable Python CI workflow.

It uses:

```yaml
on:
  workflow_call:
```

This means the workflow does not run directly on every push. Instead, another workflow can call it when needed.

The integration workflow:

- Checks out the repository
- Sets up Python
- Installs dependencies
- Runs flake8 linting
- Runs pytest
- Publishes a JUnit test report

Because this repository keeps each lab in a subfolder, the workflow runs commands inside:

```text
challenge-02-container-image
```

### Container delivery workflow

`02-container-publish.yml` is the delivery workflow.

It contains two jobs:

```text
integration
build
```

The `integration` job calls the reusable Python CI workflow:

```yaml
integration:
  uses: ./.github/workflows/02-container-python-ci.yml
```

The `build` job waits for the integration job to finish successfully:

```yaml
build:
  needs: [integration]
```

This prevents the Docker image from being built and published if the Python integration checks fail.

## Docker image build and publish

The delivery workflow builds the Docker image from the lab subfolder:

```yaml
context: ./challenge-02-container-image
file: ./challenge-02-container-image/Dockerfile
```

This is important because the application files are not stored in the repository root.

The image is published to GitHub Container Registry:

```text
ghcr.io
```

The published package is available through the repository Packages section.

## Permissions

The delivery workflow uses job-level permissions.

The integration job needs:

```yaml
contents: read
checks: write
```

The build job needs:

```yaml
contents: read
packages: write
id-token: write
```

`packages: write` allows the workflow to publish the Docker image to GitHub Packages.

`id-token: write` is used by cosign to sign the published container image.

## Result

The completed workflow performs this delivery sequence:

```text
Python integration checks
↓
Docker image build
↓
GitHub Packages publish
↓
Container image signing
```

The workflow completed successfully and published a container image package for this lab.

## Key Concepts Practiced

- Reusable workflows with `workflow_call`
- Calling one workflow from another workflow
- Workflow dependencies with `needs`
- Job-level permissions
- Docker Buildx setup
- Docker image build and push
- GitHub Container Registry publishing
- Container image signing with cosign
- Adapting GitHub Actions workflows for projects stored in subfolders

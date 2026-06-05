# Django CI Workflow

This lab implements a GitHub Actions CI workflow for a Django project. The goal is to run automated checks in a clean GitHub-hosted runner and verify that the project can install its dependencies and pass its test suite outside the local development environment.

## Project Structure

```text
challenge-01-django-ci/
├── dashboard/
├── engineering_dept/
├── marketing_dept/
├── sales_dept/
├── manage.py
├── requirements.txt
└── README.md
```

The Django project is stored in this subdirectory, while the workflow file is stored at the repository level:

```text
.github/workflows/django-ci.yml
```

Because the project is not located in the repository root, the workflow uses a working directory configuration:

```yaml
defaults:
  run:
    working-directory: challenge-01-django-ci
```

This ensures that commands such as dependency installation and test execution run from the correct project folder.

## Workflow Overview

The workflow runs on pushes and pull requests to the `main` branch.

It performs the following steps:

* checks out the repository files
* sets up Python
* installs project dependencies from `requirements.txt`
* runs the Django test suite with `python manage.py test`

The workflow also uses a matrix strategy to test the project across multiple Python versions:

* Python 3.11
* Python 3.12
* Python 3.13
* Python 3.14

## Debugging Result

The first workflow run failed during the test step. The logs showed that one test required `numpy`, but `numpy` was not listed in `requirements.txt`.

The issue was fixed by adding `numpy` to the project dependencies:

```text
Django>=5.0,<6.0
numpy
```

After updating the dependency file and pushing the change, all matrix jobs completed successfully.

## Key Concepts Practiced

* GitHub Actions workflow configuration
* CI triggers for push and pull request events
* GitHub-hosted runners
* Python setup in CI
* Dependency installation from `requirements.txt`
* Django test execution in GitHub Actions
* Matrix builds across multiple Python versions
* Reading workflow logs to identify failure causes
* Fixing missing dependency issues in a reproducible way

# OpenShift Pipelines Final Project

This repository contains a sample CI/CD configuration for a Python application using GitHub Actions and OpenShift Pipelines (Tekton).

## Project objectives

- Run Python lint checks with Flake8.
- Run unit tests with nose.
- Use Tekton tasks to clean the workspace and execute the test suite.
- Provide a Tekton Pipeline that runs cleanup before testing.

## Repository structure

```
.github/
  workflows/
    workflow.yml
.tekton/
  tasks.yml
  pipeline.yml
```

## GitHub Actions

The workflow in `.github/workflows/workflow.yml` runs on pushes and pull requests to the `main` branch. It installs the Python test tools, runs Flake8, and executes nose tests.

## OpenShift Pipelines

The Tekton definitions in `.tekton/tasks.yml` define:
- `cleanup`: removes Python cache files from the shared source workspace.
- `nose-tests`: installs Flake8 and nose, runs lint checks, and executes the nose test suite.

The pipeline in `.tekton/pipeline.yml` runs these tasks in sequence.

## Run locally

Install the tools:

```bash
python -m pip install flake8 nose
```

Run lint and tests:

```bash
flake8 .
nosetests
```

> Note: A successful workflow or OpenShift Pipeline run depends on adding the application's source code and tests, configuring the OpenShift cluster, and running the pipeline in that environment. The configuration files alone do not prove a successful run.

# Workflow-Templates

This repository contains reusable GitHub Actions workflow templates to simplify CI/CD setup across projects. These templates can be used via the `uses:` keyword in your workflows to share and centralize build logic like Docker image building and publishing.

## 📦 Included Templates

- **Docker Build and Push**  
  A reusable workflow that builds a Docker image and pushes it to GitHub Packages.

## 🚀 Example Usage

Here’s how to use the `docker-build-and-push-github.yml` template in your own repository:

```yaml
name: Build and Push {Name}

on:
  push:
    branches:
      - main
  workflow_dispatch:

permissions:
  contents: read
  packages: write

jobs:
  docker-build:
    uses: wtb04/Workflow-Templates/.github/workflows/docker-build-and-push-github.yml@main
    with:
      image-name: {Imagename}
      dockerfile: {Dockerfile location}

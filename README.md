# Workflow-Templates

This repository contains reusable GitHub Actions workflow templates to simplify CI/CD setup across projects. These templates can be used via the `uses:` keyword in your workflows to share and centralize build logic like Docker image building and publishing.

## Example

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
```

## Inputs

| Input | Required | Default | Description |
| --- | --- | --- | --- |
| `image-name` | yes | n/a | Image name under `ghcr.io/<owner>/`. |
| `dockerfile` | no | `Dockerfile` | Path to the Dockerfile. |
| `context` | no | `.` | Build context. |
| `tag` | no | `latest` | Tag for the multi-arch manifest. |
| `build-args` | no | none | Newline-separated `KEY=value` pairs passed to the build. |

### build-args

For values the build needs but the context should not carry:

```yaml
    with:
      image-name: homepage
      build-args: |
        GIT_COMMIT_SHA=${{ github.sha }}
        GIT_REMOTE_URL=${{ github.server_url }}/${{ github.repository }}
```

Read them with `ARG` in the Dockerfile. Declare the `ARG` *below* your dependency install step. A value that changes every commit invalidates every layer under it, so an `ARG` placed above `RUN npm ci` forces a reinstall on every build.

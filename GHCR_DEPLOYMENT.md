# GitHub Container Registry Deployment

This repository now includes a GitHub workflow that automatically builds and deploys Docker images to GitHub Container Registry (GHCR) in addition to the existing DockerHub deployments.

## Workflow: Deploy to GitHub Container Registry

**File:** `.github/workflows/workflow-docker-ghcr.yml`

### Triggers

The workflow is triggered by:

1. **Manual Dispatch** (`workflow_dispatch`): 
   - Allows manual execution with custom tag and platform options
   - Default tag: `latest`
   - Default platforms: `linux/amd64,linux/arm64`

2. **Tag Push**: 
   - Automatically triggered when tags are pushed to the repository
   - Uses the tag name as the image tag

3. **Branch Push** (main/master):
   - Triggered on pushes to main or master branches
   - Tagged as `latest` for the default branch

### Features

- **Multi-platform builds**: Supports `linux/amd64` and `linux/arm64` architectures
- **Automatic tagging**: Uses Docker metadata action for consistent tagging
- **Secure authentication**: Uses `GITHUB_TOKEN` for GHCR authentication
- **Build summary**: Provides detailed build information in the workflow summary

### Docker Image Location

Images are published to: `ghcr.io/thegreyfellow/arch-qbittorrentvpn`

### Usage

To pull the image from GHCR:

```bash
# Pull latest
docker pull ghcr.io/thegreyfellow/arch-qbittorrentvpn:latest

# Pull specific tag
docker pull ghcr.io/thegreyfellow/arch-qbittorrentvpn:v1.0.0
```

### Benefits over DockerHub

- **Free for public repositories**: No rate limits or pull restrictions
- **Integrated with GitHub**: Seamless authentication and permissions
- **Version control integration**: Direct link between code and container images
- **Better security**: Uses GitHub's security scanning and vulnerability detection

### Permissions

The workflow requires the following permissions:
- `contents: read` - To checkout the repository
- `packages: write` - To push images to GHCR

These are automatically granted when using `GITHUB_TOKEN`.
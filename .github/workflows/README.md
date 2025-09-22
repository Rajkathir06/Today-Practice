# GitHub Actions Workflows

## Docker Multi-Architecture Build

This repository now uses GitHub Actions to build Docker images with multi-architecture support (AMD64 and ARM64).

### Migration from Travis CI

- **Before**: Travis CI built single-architecture images only
- **After**: GitHub Actions builds both AMD64 and ARM64 architectures

### Required Secrets

Configure these secrets in the repository settings:

- `DOCKER_USERNAME`: Docker Hub username
- `DOCKER_PASSWORD`: Docker Hub access token

### Build Triggers

- **Push to master**: Builds and publishes all image variants
- **Pull requests**: Builds images for testing (no push)
- **Weekly schedule**: Rebuilds to catch upstream Node.js updates

### Supported Architectures

All images now support:
- `linux/amd64` (Intel/AMD 64-bit)
- `linux/arm64` (ARM 64-bit, including Apple Silicon)

### Matrix Strategy

The workflow builds all combinations of:
- Node versions: 18, 20, 22, 24, latest
- Variants: alpine, bookworm, bullseye, buster, slim

Some combinations are excluded for compatibility reasons (e.g., buster with Node 22+).
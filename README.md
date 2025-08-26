# Docker Hardened Images for Codespaces

This repository demonstrates how to set up a customized Docker Hardened Image (DHI) environment for GitHub Codespaces using a layered approach with multiple DHI variants.

## Overview

This setup provides a secure, production-ready development environment by combining Docker Hardened Images with GitHub Codespaces. The configuration creates a custom container that leverages Docker's enterprise-grade security features while maintaining developer productivity.

## Architecture

The custom image is built using a layered approach:

1. **Base Layer**: `dhi-node` Debian-dev variant
2. **Overlay Layer**: `dhi-python` Debian-dev variant (applied via OCI artifacts)
3. **Package Layer**: Additional custom packages not included in base images
4. **User Configuration**: Declared user aand group

## Repository Structure

```
├── .devcontainer/
│   └── devcontainer.json  # Codespaces configuration
│   └── Dockerfile  # Dockerfile to run ldconfig
└── README.md              # This file
```

## Key Components

### Dockerfile
The Dockerfile achieves two objectives:
- Defined the custom image that will be used in the FROM statement
- Runs ldconfig to generate the /etc/ld.so.cache, which is required by Devcontainers/Codespaces

### devcontainer.json
Configures the Codespaces environment to:
- Specify that the container will be built via Dockerfile
- Set up the containerEnv with variables that will need to be populated in the Project's Settings, under Secrets and Variables -> Codespaces.
- Ensure that you project has two Codespaces secrets: DOCKER_USERNAME and REGISTRY_TOKEN (PAT)
- The previous two steps will allow Codespaces to pull the image from the private repo in Docker Hub.

## Details about the DHI Customization Flow

This repository implements Docker's DHI customization flow using three main options:

### 1. OCI Artifacts Option
- Overlays `dhi-python` Debian-dev variant on top of `dhi-node` base Debian-dev variant
- It's important to ensure compatibility between different DHI image variants. Use all Debian or all Alpine, of the same version.
- Maintains security hardening across layers

### 2. Packages Option
- Installs additional packages not available in base DHI images
- Customizes the environment for specific development needs
- Preserves security compliance during package installation

### 3. User Declaration
- Defines user accounts and groups
- 
## Getting Started

### Prerequisites
- Access to Docker Hardened Images
- Appropriate permissions to create a custom DHI image
- GitHub Codespaces enabled on your account

### Usage

1. **Fork or clone this repository**
   ```bash
   git clone <repository-url>
   ```

2. **Open in Codespaces**
   - Navigate to the repository on GitHub
   - Click "Code" → "Codespaces" → "Create codespace on main"
   - Wait for the container to build and start

3. **Customize as needed**
   - You can built variants for this customization as needed using the DHI customization flow
   - Update `devcontainer.json` for specific Codespaces settings or for access to different repos

## Benefits

- **Security**: Leverages Docker Hardened Images for enterprise-grade security
- **Flexibility**: Combines multiple DHI variants for comprehensive tooling
- **Consistency**: Ensures identical development environments across team members
- **Compliance**: Maintains security standards while enabling development workflows
- **Efficiency**: Pre-configured environment reduces setup time

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test in Codespaces
5. Submit a pull request

## Support
- Open a Github Issue

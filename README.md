# build-agents
I have an on premise Kubernetes cluster at home. This cluster runs services for my family and friends, useful tools for me to use and acts as a sandbox for me to learn. This project falls in the latter two categories.

#### Status
[![build-agents](https://github.com/clincha/build-agents/actions/workflows/build-agent-ubuntu.yml/badge.svg)](https://github.com/clincha/build-agents/actions/workflows/build-agent-ubuntu.yml)

## Getting Started
The GitHub Actions workflow runs a job that builds the Ubuntu GitHub Actions Docker image and then pushes the image to GitHub. A self-hosted runner then applies the Kubernetes deployments to the Kubernetes cluster at home.

The best place to start looking is in
`build-agents/.github/workflows/build-agent-ubuntu.yml` This file explains the overall process and guides you along to the others through the process.

The deployments folder has customised deployments for each repository that uses agents. The structure for a filename goes `distro-repository.yml` so that `ubuntu-build-agents.yml` is the filename for this repositories build agents.

### Adding more repositories
Copy an existing deployment's YAML file and replace these environment variables:
- GH_REPOSITORY
- GITHUB_OWNER
- GITHUB_REPOSITORY

Replace all instances of the existing deployments name with a name for the new deployment (see above for naming convention).

Commit and push to the build-agents repository.

### Adding more distributions
I donno, I'll let you know when I get there ;)

### Secrets
The following secrets need to be set in the build-agents GitHub repository:
- DOCKER_PASSWORD (https://www.docker.com/)
- GH_PAT_TOKEN (https://github.com/settings/tokens)
- KUBECONFIG (~/.kube/config)
# docker-dev-env-openfaas

Custom base image to create a [Docker Dev Environment](https://docs.docker.com/desktop/dev-environments/) and start developing OpenFaaS functions quickly.

## Introduction

The ultimate goal is to provide a dev environment container with all the dependencies needed to build and run OpenFaaS functions.

## Dependencies included in the base image

- [Arkade](https://github.com/alexellis/arkade)
- [OpenFaaS CLI](https://github.com/openfaas/faas-cli)
- kubectl
- docker CLI tools

## Example

Create a Dev Environment from repo X
If you have Docker installed, then you can install Kubernetes using KinD in a matter of moments:
`kind create cluster`

Install OpenFaaS with `arkade` which is already in the base image: `arkade install openfaas`

- TODO:

- [ ] GH Action to build multiarch.
- [ ] Create OpenFaaS hello world demo repository with `.docker` folder.
- [ ] Add `make`, `go`, `gpg`?

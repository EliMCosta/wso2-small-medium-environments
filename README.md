 # Docker and Docker Compose Resources for WSO2 API Manager

This repository contains following Docker resources:

- CentOS based Docker resources for WSO2 API Manager

- Docker Compose resources for the Single Node deployment pattern (see https://apim.docs.wso2.com/en/latest/install-and-setup/setup/single-node/all-in-one-deployment-overview/).

## Use cases
- Non-production environments
- Small production environments

Docker resources for WSO2 API Manager help you build generic Docker images for deploying the corresponding product servers in containerized environments.

Each Docker image includes the Java Development Kit, the relevant product distribution and a collection of utility libraries.
Configurations and non-configuration resources (e.g. binaries such as, third-party libraries, Carbon extensions, Carbon Applications and security related artifacts such as, Java Keystore files) are designed to be provided via volume mounts to the containers spawned.

## Steps
- Build the software artifacts (see BUILD_ARTIFACTS.md file on this folder)
- Build the wso2am docker image according to docker/README.md
- Up the docker-compose.yml




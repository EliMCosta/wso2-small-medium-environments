# Docker Image for WSO2 API Manager #

This section defines the step-by-step instructions to build an [CentOS](https://hub.docker.com/_/centos/) Linux based Docker image for WSO2 API Manager 4.2.0.

## Prerequisites

* [Docker](https://www.docker.com/get-docker) v17.09.0 or above
* [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) client


## How to build an image and run

> The local copy of the `dockerfiles/centos/apim` directory will be referred to as `AM_DOCKERFILE_HOME` from this point onwards.

#### 1. Build the Docker image.

- Navigate to `<AM_DOCKERFILE_HOME>` directory. <br>
- Change <APIM_DIST_URL> in Dockerfile to the URL of the product pack. You can use our zip if you don't want build your own: https://github.com/EliMCosta/wso2-small-medium-environments/releases/download/v4.2.0/wso2am-4.2.0.zip
  
  Execute `docker build` command as shown below.

```
docker build -t localhost/wso2am:4.2.0-centos-jdk11 .
```

#### 2. Running the Docker image.

```
docker run -it -p 9443:9443 -p 8243:8243 localhost/wso2am:4.2.0-centos-jdk11
```

> Here, only port 9443 (HTTPS servlet transport) and port 8243 (Passthrough or NIO HTTPS transport) have been mapped to Docker host ports.
You may map other container service ports, which have been exposed to Docker host ports, as desired.

#### 3. Accessing management console.

- To access the management console, use the docker host IP and port 9443.
    + `https://<DOCKER_HOST>:9443/carbon`
    
> In here, <DOCKER_HOST> refers to hostname or IP of the host machine on top of which containers are spawned.

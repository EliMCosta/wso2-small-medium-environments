# Dockerfile for WSO2 API Manager #

This section defines the step-by-step instructions to build an [CentOS](https://hub.docker.com/_/centos/) Linux based Docker image for WSO2 API Manager 4.2.0.

## Prerequisites

* [Docker](https://www.docker.com/get-docker) v17.09.0 or above
* [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) client


## How to build an image and run

> The local copy of the `dockerfiles/centos/apim` directory will be referred to as `AM_DOCKERFILE_HOME` from this point onwards.

#### 1. Build the Docker image.

- Download wso2am-4.2.0.zip from [here](https://wso2.com/api-management/install/)
- Navigate to `<AM_DOCKERFILE_HOME>` directory. <br>
- Change <APIM_DIST_URL> in Dockerfile to the URL of the product pack.
  Execute `docker build` command as shown below.

```
docker build -t localhost/wso2am:4.2.0-centos-jdk11 .
```

> By default, the Docker image will prepackage the General Availability (GA) release version of the relevant WSO2 product.

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

## How to update configurations

Configurations would lie on the Docker host machine and they can be volume mounted to the container. <br>
As an example, steps required to change the port offset using `deployment.toml` is as follows:

#### 1. Stop the API Manager container if it's already running.

In WSO2 API Manager version 4.2.0 product distribution, `deployment.toml` configuration file <br>
can be found at `<DISTRIBUTION_HOME>/repository/conf`. Copy the file to some suitable location of the host machine, <br>
referred to as `<SOURCE_CONFIGS>/deployment.toml` and change the offset value (`[server]->offset`) to 1.

#### 2. Grant read permission to `other` users for `<SOURCE_CONFIGS>/deployment.toml`.

```
chmod o+r <SOURCE_CONFIGS>/deployment.toml
```

#### 3. Run the image by mounting the file to container as follows:

```
docker run -it \
-p 9444:9444 \
-p 8244:8244 \
--volume <SOURCE_CONFIGS>/deployment.toml:<TARGET_CONFIGS>/deployment.toml \
wso2am:4.2.0-centos-jdk11
```

> In here, <TARGET_CONFIGS> refers to /home/wso2carbon/wso2am-4.2.0/repository/conf folder of the container.


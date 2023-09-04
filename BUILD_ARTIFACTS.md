# Building WSO2 APIM binaries from Source

To build the WSO2 APIM binaries executable from the source code, follow the steps below:

## Install the required dependencies

- Ensure you have Git installed on your system. You can install it via your distribution's package manager.
- Install JDK 11. You can install it via your distribution's package manager.
- Install the latest version of Apache Maven. You can install it via your distribution's package manager.

## Clone the repository and select the latest stable version

1. Open the terminal and navigate to the folder where you wish to clone the repository.
2. Run the following command to clone the repository: git clone https://github.com/wso2/product-apim.git
3. After cloning, enter the cloned directory with: cd product-apim
4. Switch to the desired tag with the command: git checkout tags/v4.2.0

## Build the WSO2 API Manager

1. In the terminal, while in the cloned repository folder, run the following command on root folder to build the project: mvn clean install -Dmaven.test.skip=true. The build might take some time depending on your machine. Maven will download the necessary dependencies and build the project.
2. Once the build is complete, you should find the executable (wso2am-4.2.0.zip) in the "modules/distribution/product/target" folder within the project directory.

Note 1: It is recommended to have at least 6vCPU and 12GB RAM to ensure your local machine doesn't freeze and isn't used for other tasks while the build is in progress.
Note 2: Eventually, you might need to restart the build since various downloads are made during the process (it should take a few minutes), and sometimes WSO2 servers stop responding.


### Build on Rocky Linux 8 server with openJDK11, Git and Maven installed from system repositories - 8vCPU/16GB RAM

```
mkdir ~/wso2am-tmp && cd ~/wso2am-tmp
```
```
git clone https://github.com/wso2/product-apim.git
```
```
cd product-apim && git checkout tags/v4.2.0
```
```
sudo mvn clean install -Dmaven.test.skip=true
```
[...]


You can now upload the ziped artifacts (located on <PROJECT_ROOT_DIRECTORY>/modules/distribution/product/target) to your project repositories.

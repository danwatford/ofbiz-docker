# Ofbiz Docker Seed
A project to build docker images of Apache Ofbiz with your chosen plugins. 

## Aim
To provide a quick way to *dockerise* Ofbiz for demonstration or deployment for testing.

## Provides
This project produces docker images based on sources that are checked out to the workspace as submodules. This means 
changes in the workspace can be incorporated into built docker images.

## Usage
Clone this project, with recursion into submodules:
```shell script
git clone --recurse-submodules http://github.com/danwatford/TODO
```
Modify the variables at the top of `build.gradle` as appropriate for your project.

Build the docker container image:
```shell script
./gradlew buildOfbizImage
```

List the new docker image
```shell script
docker images
```

Run the image:
```shell script
docker-compose up
```

Visit https://localhost:8443/partymgr and login with username `admin` and password `ofbiz`.
You may need to accept the browsers warning that the connection is not secure.

Stop the container buy interrupting (Ctrl-C) the docker-compose process or runnng `docker-compose down`.

## Setup and maintenance
Ofbiz-framework was linked to this project as a git submodules using the following command:
```shell script
git submodule add -b trunk https://github.com/apache/ofbiz-framework
```

If developing a plugin we cannot link this as a submodule directly under ofbiz-framework/plugins since any nested
submodules must be specified by the ofbiz-framework repository.

Instead we can clone the plugin's git repository to ofbiz-framework/plugins. The downside if using this project as part
of a CI/CD build is that we will need to add additional external steps to close the repository. See 
`azure-pipelines-ofbiz-image.yml` for how this can be done using Azure DevOps.

As an exmaple, the GridTest plugin can be added using the following commands:
```shell script
mkdir ofbiz-framework/plugins

git clone https://github.com/danwatford/ofbizGridTest ofbiz-framework/plugins/gridTest
```


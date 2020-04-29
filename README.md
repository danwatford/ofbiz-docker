# Ofbiz Docker Seed
A project to build docker images of Apache Ofbiz with your chosen plugins. 

## Aim
To provide a quick way to *dockerise* Ofbiz for demonstration or deployment for testing.

## Provides
This project creates docker images based on sources that are checked out to the workspace. This means 
changes in the workspace can be incorporated into built docker images.

## Usage
Clone this project and change to the project directory. Example:
```shell script
git clone https://github.com/danwatford/ofbiz-docker

cd ofbiz-docker
```

Clone the wanted branch of ofbiz-framework. Example:
```shell script
git clone https://github.com/apache/ofbiz-framework --branch trunk
```

Clone any wanted plugins to the ofbiz-framework/plugins directory. Example:
```shell script
mkdir ofbiz-framework/plugins

git clone https://github.com/danwatford/ofbizGridTest ofbiz-framework/plugins/gridTest
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
Depending on your docker setup, you may need to substitute localhost for your docker-machine's IP address.
You may also need to accept the browser's warning that the connection is not secure.

Stop the container buy interrupting (Ctrl-C) the docker-compose process or runnng `docker-compose down`.

# docker-ionic-cordova

Docker image for building [Ionic](https://ionicframework.com/) apps with [Cordova](https://cordova.apache.org/).

## How to use this image

### Build image

Build from [GitHub](https://github.com/soiqualang/docker-ionic-cordova):  
```bash
docker build -t soiqualang/ionic-cordova github.com/soiqualang/docker-ionic-cordova

# or
docker build -t ionic_env .
```

Available build arguments:

- JAVA_VERSION
- NODEJS_VERSION
- ANDROID_SDK_VERSION
- ANDROID_BUILD_TOOLS_VERSION
- IONIC_CLI_VERSION
- CORDOVA_CLI_VERSION

### Run image

Run the docker image:  
```bash
docker run -it soiqualang/ionic-cordova
```

> test

```bash
# Run
docker run --name ionic_env -it --net=host -v D:/sync/websvr/ionic:/workdir ionic_env bash

docker run --name ionic_env -it -p 8100:8100 -v D:/sync/websvr/ionic:/workdir ionic_env bash

# Access container
docker exec -it ionic_env /bin/bash

# Make new app
# https://ionicframework.com/docs/cli/commands/start

ionic start myApp tabs --cordova
```

## CI Configuration

### GitLab

Here is a sample `.gitlab-ci.yml` file:

```yml
image: soiqualang/ionic-cordova

stages:
    - build

build_android:
    stage: build
    cache:
        paths:
            - node_modules/
            - plugins/
    script:
        - npm ci
        - ionic cordova build android
    artifacts:
        paths:
            - platforms/android/app/build/outputs/apk/debug
```

## Questions / Issues

If you got any questions or problems using the image, please visit my [GitHub Repository](https://github.com/soiqualang/docker-ionic-cordova) and write an issue.

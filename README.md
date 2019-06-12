# Purpose

This repository shows how to dockerize a quarkus project without running maven in local machine. It shows that using multi-stage builds is a better alternative.

## Classic way (Quarkus' way)

### Creating Docker Image with Runnable JAR

- Run mvn to create JAR file
```
./mvnw package 
```

- Run docker to build an image with the created JAR file
```
docker build -f Dockerfile.jvm -t quarkus-quickstart/getting-started-jvm .
```

- Run a container with the image
```
docker run -i --rm -p 8080:8080 quarkus-quickstart/getting-started-jvm:latest
```
### Creating Docker Image with Native Binary

- Run mvn to create JAR file and then to run a docker container to create native binary
```
./mvnw package -Pnative -Dnative-image.docker-build=true
```

> For `native` profile, mvn run a docker image to create a native binary from JAR file. I believe running `docker run` via mvn is not a good idea.

- Run docker to build an image with the created JAR file
```
docker build -f Dockerfile.native -t quarkus-quickstart/getting-started-native .
```

- Run a container with the image
```
docker run -i --rm -p 8080:8080 quarkus-quickstart/getting-started-native:latest
```

<br><br><br>

## Modern way (My proposal)


### Creating Docker Image with Runnable JAR

- Run docker to build an image with runnable JAR
```
docker build -f Dockerfile.proposed.jvm -t quarkus-quickstart/getting-started-proposed-jvm .
```

- Run a container with the image
```
docker run -i --rm -p 8080:8080 quarkus-quickstart/getting-started-proposed-jvm:latest
```
### Creating Docker Image with Native Binary

- Run docker to build an image with native binary
```
docker build -f Dockerfile.proposed.native -t quarkus-quickstart/getting-started-proposed-native .
```

- Run a container with the image
```
docker run -i --rm -p 8080:8080 quarkus-quickstart/getting-started-proposed-native:latest
```
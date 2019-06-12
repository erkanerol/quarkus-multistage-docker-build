# Purpose

This repository shows how to dockerize a quarkus project without running maven in local machine.

## Classic way (Quarkus' way)

### Runnable JAR

- Run mvn to create JAR file
```
./mvnw package 
```

- Run docker to build an image with the created JAR file
```
docker build -f Dockerfile.jvm -t quarkus-quickstart/getting-started-jvm .
```

- Run a container
```
docker run -i --rm -p 8080:8080 quarkus-quickstart/getting-started-jvm:latest
```
### Native

- Run mvn to create JAR file and then to run a docker container to create native binary
```
./mvnw package -Pnative -Dnative-image.docker-build=true
```

> I believe running `docker run` via mvn is not a good idea.

- Run docker to build an image with the created JAR file
```
docker build -f Dockerfile.native -t quarkus-quickstart/getting-started-native .
```

- Run a container
```
docker run -i --rm -p 8080:8080 quarkus-quickstart/getting-started-native:latest
```

## Modern way (My proposal)



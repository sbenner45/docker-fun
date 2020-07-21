# Docker-fun
Overview of what Docker containers are. [what-is-a-container](https://www.docker.com/resources/what-container)

## Docker Images
Docker applications at rest are Docker images. 

### What is an Image
Docker images are read-only instructional objects that are used by the Docker daemon to create containers. 

### Create a new Image
Docker images are created/customized using a __dockerfile.__ 
Dockerfile Example
```bash
```

### Managing Images
Download an image:
```bash
docker image pull nginx:1.14.0
```

List images on the system:
```bash
docker image ls
docker image ls -a
```

Inspect image metadata:
```bash
docker image inspect nginx:1.14.0
docker image inspect nginx:1.14.0 --format "{{.Architecture}}"
docker image inspect nginx:1.14.0 --format "{{.Architecture}} {{.Os}}"
```

Delete an image:
```bash
docker image rm nginx:1.14.0
```

Force deletion of an image that is in use by a container:
```bash
docker run -d --name nginx nginx:1.14.0
docker image rm -f nginx:1.14.0
```

Locate a dangling image and clean it up:
```bash
docker image ls -a
docker container ls
docker container rm -f nginx
docker image ls -a
docker image prune
```

#### Using Docker Trusted Registry
Login
Organizations
Repositories

#### Pulling from DTR
Try docker login:
```bash
docker login <registry public hostname>
```

Push to and pull from your private registry:
```bash
docker pull ubuntu
docker tag ubuntu <registry public hostname>/ubuntu
docker push <registry public hostname>/ubuntu
docker image rm <registry public hostname>/ubuntu
docker image rm ubuntu
docker pull <registry public hostname>/ubuntu
```

## Docker Storage
### Docker volumes
### Clustered storage

## Docker Networking
### Networking Basics

## Docker UCP
### User set-up
#### Create Bundle

## Orchestration
### Docker Services
### Docker Compose
### Docker Stacks

## Docker Troubleshooting
### Container Logs
### Container Monitoring
### Container Communication
### UCP Node reporting Unhealthy

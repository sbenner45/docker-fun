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
Storage Drivers aka graph drivers. overlay2, aufs, devicemapper  
Storage models - persistent data can be managed using several storage models.
* Filesystem storage
  * Data is stored in the form of a file system.
  * Used by overlay2 and aufs.
  * Efficient use of memory.
  * Inefficient with write-heavy workloads.
* Block storage
  * Stores data in blocks
  * Used by devicemapper
  * efficient with write-heavy workloads
* Object storage
  * Stores data in an external object-based store
  * Application must be designed to use object-based storage
  * Flexiable and scalable

### Locate Docker Storage
Run a basic container:
```bash
docker run --name storage_nginx nginx
```
Use docker inspect to find the location of the container's data on the host:
```bash
docker container inspect storage_nginx
ls /var/lib/docker/overlay2/<STORAGE_HASH>/
```
Use docker inspect to find the location of an image's data:
```bash
docker image inspect nginx
```

### Docker Mounts & Volumes
There are two ways of using external storage for Docker containers:
* Bind mounts
* Volumes
Bind mounts
* mount point that is locate on the system
* not considered portable, relies on the host file system and directory structure
Volumes
* Docker managed storage, which is on the host system
* considered to be portable
* can be utilitzed by multiple containers
* more flexiable than bind mounts

## Docker Networking
__bridge:__ The default network driver. If you don’t specify a driver, this is the type of network you are creating. Bridge networks are usually used when your applications run in standalone containers that need to communicate. See bridge networks.

__host:__ For standalone containers, remove network isolation between the container and the Docker host, and use the host’s networking directly. host is only available for swarm services on Docker 17.06 and higher. See use the host network.

__overlay:__ Overlay networks connect multiple Docker daemons together and enable swarm services to communicate with each other. You can also use overlay networks to facilitate communication between a swarm service and a standalone container, or between two standalone containers on different Docker daemons. This strategy removes the need to do OS-level routing between these containers. See overlay networks.

__macvlan:__ Macvlan networks allow you to assign a MAC address to a container, making it appear as a physical device on your network. The Docker daemon routes traffic to containers by their MAC addresses. Using the macvlan driver is sometimes the best choice when dealing with legacy applications that expect to be directly connected to the physical network, rather than routed through the Docker host’s network stack. See Macvlan networks.

__none:__ For this container, disable all networking. Usually used in conjunction with a custom network driver. none is not available for swarm services. See disable container networking.

__Network plugins:__ You can install and use third-party network plugins with Docker. These plugins are available from Docker Hub or from third-party vendors. See the vendor’s documentation for installing and using a given network plugin.


### Docker Network summary
__User-defined bridge__ networks are best when you need multiple containers to communicate on the same Docker host.  
__Host networks__ are best when the network stack should not be isolated from the Docker host, but you want other aspects of the container to be isolated.  
__Overlay networks__ are best when you need containers running on different Docker hosts to communicate, or when multiple applications work together using swarm services.  
__Macvlan__ networks are best when you are migrating from a VM setup or need your containers to look like physical hosts on your network, each with a unique MAC address.  


## Docker UCP
Navigating the UCP

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

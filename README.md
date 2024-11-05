# docker-notes

### What is Docker:
* Containerization is a conecept or technology and docker implements containerization.
  Docker is a Containerization platform that provides easy way to containerize our applications, which means using docker you can create build the container images, run the images to create containers and also push the containers to container registries such as Dockerhub,quay.io, ECR and so on

### Container :
* A container is a bundle of application, application libraries required to run our application and the minimum system dependencies.
  A container is a standard unit of software that packages up code and all its dependencies so the application runs quickly and realiably from other computing environment.
  Docker container is a running instance of a image.

### Containers vs Virtual machines :
- containers and Vm's are both techonologies used to isolate applications and their dependencies, but they have some key differences:

Resource-utilization:
- containers share the the host OS kernel, making them lightweight and faster than VM'share
- Vm's have full-pledged OS&hypervisior making them some resource intensive.
   
Portability:
- containers are designed to be portable & can run on any system with a compatible host OS.
- VM are less portable as they need compatible hypervisior to run.
   
Security:
- Container are less isolation, as they share host OS.
- VM's provide high security as they have own OS.
   
Management:
- Managing containers is typically easier than managing VM's as containers are designed to be light-weight and fast moving.


### Docker life cycles:
- There are important things:
  - DockerBuild : Builds docker images fron docker file
  - DockerRun : Runs containers from docker images.
  - DockerPush : Push the container image to registry to share iamge

### Docker architecture :
- Docker uses a client-server architecture.The docker client talks with the docker daemon which helps in building, running and distributing the docker containers. Daemon/sever responds to client instructions and acts accordingly.
  - Docker Client : Docker commands
  - Docker Daemon : Docker Engine


### Docker Instuctions :
 - FROM : FROM instruction should be the first to represent base OS 
  - RUN : To install packages and cconfigure them, will excute at the time of image creation
  - CMD : Run at the time of container creation
  - ENTRYPOINT : Excute at time of container creation, helps to overwtitten CMD
  - Label : Key value pair, useful for filtering objects
  - ENV : Key value pair, can be accessed inside container to use
  - ARG : To supply argument to the iamges( pass args --build-arg)
  - EXPOSE : Provides information, On what port continer is running
  - COPY : To add files from workspace to images
  - ADD : To add files from workspace & internet
  - USER : Dokcer container should never run with root user , so create user with USER instruction
  - WORKDIR : Sets the present working directory
  - ONBUILD : Someone is try to use our image at that time onbuild instruction will run


### CMD vs ENTRYPOINT :
* CMD instruction can be overwtitten, but ENTRYPOINT cannot be overwtitten. If we try to do it will go and append.
    But we can mix CMD & ENTRYPOINT for better results.
	CMD is used to supply default arguments to ENTRYPOINT, we can always override default args from runtime.
	Ex : CMD ["google.com"] || ENTRYPOINT ["ping", "-c5"]
         Docker run <image-id>:1.0 yahoo.com - CMD overwtitten
		 Docker run <image-id>:1.0 google.com - Default

### COPY vs ADD :
- copy and add are to copy files from workspace to docker iamge. But add have to extra advantages
  - It can directly download content from internet into iamges
  - It can directly untart files into images/folders  
  


### ENV vs ARG  :
-  ENV variables can be accessed both at the time of build images and contianer, can be accessed inside container
  - ARG can be accessed both at the time of build images , arg can't be accessed inside container
    ARG can be used in one exceptional case to keep before FROM instruction, to supply argument to FROM instruction for base OS version.


### Dockerfile :
* It is declarative way of creating custom images( Keeping all the instructions in a file i.e.., docker file and build images)


### Docker compose :
* Docker compose is a tool where we can define all service up and down at a time, we can create dependices between the services and also we can create the networks and volumes

### Docker Volumes :
- Containers are ephemral by default, once we remove the container it will remove the data associated to containers. To save storage we can create volumes(v) and mount(-v). Vloumes are two types; named, unnamed
 - named : Volumes are created and managed by dokcer itself
 - unnamed : Volumes are created and managed by ourself


### Docker multi-stage :
* Using multi-stage builds we can create images, we can run one dockerfile as build get the output from it, copy it to the second image and create light weight images


### Docker best Practises:
 - Use official iamges
  - keep image size small
  - use multi-stage builds
  - tag images properly
  - use dockerignore
  - Run as non-root user
  - limit continaer resources
  - network configuration
  - security best practise

### Docker Disadvantages :
  - scalibility
  - non reliable/self healing 
  - no proper volume managemnet
  - no auto scaling
  - no secrets & configuration mangement
  - complex networking

### Sample docker file for nginx :
* FROM alamalinux:9
RUN dnf install nginx -y
RUN ["nginx","-g","deamon off;"]
EXPOSE 80/tcp  




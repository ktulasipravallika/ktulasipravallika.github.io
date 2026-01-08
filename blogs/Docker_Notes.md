## Containers

## Containerisation

## Docker

## Docker Lifecycle

* **Docker File** is A text file describing how to build an image.
 
    * `FROM` → Indicates the base image.
    * `COPY` → To copy files into image.
    * `ADD` →
    * `RUN` → Commands to be executed during the build-time(during image creation)
    * `CMD` → Default runtime command contains the default arguments/commands that can be overridden(executes during the container start)
    * `ENTRYPOINT` → Main Command to be executed in the container.
    * `EXPOSE` → Documents which port the app listens on. It doesn’t open the port and publishing is done with docker run -p.
   * `docker build` → Turns Dockerfile into an image.
     
* **Docker Images**
    * Image is like a blue print and these are immutable and versioned.
    * Example: ngnix:latest
    * Commands :
        * `docker images` → Gives the list of all the images in the system.
        * `docker pull docker pull tulasipravallika/my-first-docker-image:latest` → Pull the docker image from the docker hub.
        * `docker push tulasipravallika/my-first-docker-image:tagname` → Pushes the images from the local to the docker hub.
     * `docker run` → Starts a container from an image.
       
* **Docker Containers**
    * Containers are running instances of an image.
    * Containers are ephemeral (created/destroyed/replaced easily) in nature and are light weight.
    * Once the image is executed, it creates a container process.
    * When the container process is restarted the new run time state is created, the memory/PID are reset but the container's writable layer and volumes remains same.
    * Whent he container is deleted the writable layer is lost, data in volumes statys.
    * Commands :
        * `docker ps` → Gives the list of containers running in the system.
        * `docker ps -a` → Gives the list of all the containers(running and stopped) in the system.   
        * `docker stop container_id` → Stops the running container.
        * `docker rm container_id` → removes the container completely.
        * `docker run -d --name applciation1 image_name:tag` → Runs the image and creates a container. { `-d` → Detached Mode, `--name` → `Name of the container`}
        * `docker run -d --name applciation2 image_id` → Runs the image and creates a container. { `-d` → Detached Mode, `--name` → `Name of the container`} 

* **Docker Ports**
   * Container has its own network namespace.
      * `-p 8080:80` maps the host port 8080 → container port 80

* **Docker Volumes**
  * Make data persistent / share host files into container.
 
    
## Multistage Docker Builds

    * Creating multiple stages for security and reducing the size of the images this is used.
    * The final image will contain only the required amount of runtime.
    * Only the final stage is build and the image is created.

## Distroless Docker Images

## Docker Network

   * A container has its own network namespace (its own “mini machine” networking).
   * **Bridge Network:**
      * This is the default network.
      * Containers get a private IP on a virtual bridge.
      * Outboud internet works via NAT.
      * Inbound host/extenal needs -p.
      * Commands :
         * `docker network ls` → Lists all the networks.
         * `docker network inspect bridge` → Detailed information of the network.
        
   * **User Defined Bridge Network**
      * Built-in DNS by container name, better isolation, easier networking than default bridge.
      * Commands:
         * `docker network create appnet` → Creates a new network with name appnet.
         * `docker network connect network_name container_name` → Connects the container to the network dynamically.
     
   * **Host Network**
      * Container shares the host network stack.
      * No NAT, no separate container IP.
      * No port mapping needed.
      * Commands:
         * `docker run -d --name container_name --network host nginx` 
    
   * **None**
      * 
   * **Overlay Network**
        
## Docker Volumes

   * Container filesystems are ephemeral.
   * So volumes/bind mounts are used for persistent data.
   * In prod: EBS/EFS or managed DB.
   * Avoid storing important state inside container.
   * Commands:
      * docker run --rm -v myvol:/data alpine sh -c 'echo hello > /data/a.txt'

## Docker Bind Mounts

## Docker Compose

## Docker init

* This ONLY works with on Docker Desktop.
* 

## Commands

  * `docker login`
        * Enable to login to the docker hub account and fetches the images from there on `docker pull..`.
   
  * `docker pull docker pull tulasipravallika/my-first-docker-image:latest`
        *  Pull the docker image from the docker hub.

  * `usermod -aG docker ec2-user`
        * Add the user `ec2-user` to the docker group. This enables to directly execute the commands without `sudo`.
   
  * `docker images`
        * Gives the list of all the images in the system.
   
  * `docker ps`
        *  Gives the list of containers running in the system.
   
  * `docker ps -a`
        *  Gives the list of all the containers(running and stopped) in the system.
   
  * `systemctl start docker`
        *  Starts the docker process.
   
  * `systemctl status docker` 
        * To Check the status of the docker process.
   
  * `systemctl stop docker`
        * Stops the docker process.
   
  * `docker build -t image_name:tag .`
        * Reads the Dockerfile, context, executes steps, produces an image.
        * `-t` → tag the image with a name (and optional version tag).

  * `docker run -d -p hostPort:containerPort --name applciation1 image_name:tag` 
        * Creates a container from the image_name:tag_name and starts it.
        * `-d` → Detached Mode
        * `--name` → `Name of the container`
        * `-network` → Indicates the network on the container.
        * `-e KEY=VALUE` → To set any environmental variables.
        * `-v path` → 
        * `-p` → Publishes the port
           * `hostPort` → inside the container
           * `containerPort` → If you want to reach the application from outside, you map a host port to the container port.
   
  * `docker run image_id`
       * Can also indicate image id.
         
   * `docker exec -it container_id sh`
        * Enters the container and executes any commands as required.
        * `exit` → To exit from the container. 
        * `-i` → interactive (keeps STDIN open so you can type)
        * `-t` → tty (allocates a pseudo-terminal so it feels like a real shell)
                
  * `docker stop container_id`
        *  Stops the running container.
   
  * `docker rm container_id`
        * Removes the container completely.

  * `docker tag image_name tag_name`
        * Creates an additional name (alias) for an existing image ID (no rebuild).
   
  * `docker port container-name`
        * Gives the port information and mapping.
   
  * `docker network create appnet`
        * Creates a new network with name appnet.
   
  * `docker stats`
        * Gives the information of CPU, MEM Usage and Pids and other details related to containers.
    
  * `docker logs container_id`
        * Gives the logs of the container.
 
  * `docker push tulasipravallika/my-first-docker-image:tagname`
        * Pushes the images from the local to the docker hub.
       
  






 

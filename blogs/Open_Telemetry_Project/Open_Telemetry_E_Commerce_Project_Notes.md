## Prerequisites / Tool Installation

### Docker Installation (Ubuntu)
Follow the official Docker Engine install guide:  
https://docs.docker.com/engine/install/ubuntu/#installation-methods

---

### kubectl Installation (Linux)
Use the official Kubernetes guide to install `kubectl`:  
https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/#install-kubectl-binary-with-curl-on-linux

---

### Terraform Installation
Install Terraform using HashiCorp’s official steps:  
https://developer.hashicorp.com/terraform/install

---

## OpenTelemetry Demo Project

Project repo:  
https://github.com/ktulasipravallika/ultimate-devops-project-demo

---

## Clone the Project

```
git clone https://github.com/ktulasipravallika/ultimate-devops-project-demo.git
cd ultimate-devops-project-demo/src
```

---

## Product Catalog Service (Containerization)

This repo contains ~20 microservices. For now, we will containerize only the **Product Catalog Service**.

---

### Steps

* Navigate to the `product-catalog` service folder
  ```
  cd product-catalog/
  ```
  
* Read the `README.md` of the product-catalog service to confirm the build instructions.

---

**LOCAL EXECUTION**

* Run the commands below (as mentioned in that README):
  ```
  export PRODUCT_CATALOG_PORT=<any-unique-port>
  go build -o product-catalog .
  ```
* For Go services, dependencies are automatically pulled during build.
    `go build -o product-catalog .`
     (-o specifies the name of the output binary. After the command runs successfully, a product-catalog binary is created in the current directory.)

* To run the binary file.
    `./product-catalog ` - This executes the service and outputs the below lines as mentioned in the README.md of the service.
    ```
    INFO[0000] Loaded 10 products                           
    INFO[0000] Product Catalog gRPC server started on port: 8088 
    ```
---

**Notes**

- Install `Go` if it’s not already installed:  
  ```
  sudo apt install golang-go
  go version  
  ```
- Dependencies vary by language and are usually defined in standard files:
- **For Example**
    * **Python**: requirements.txt
    * **Java**:
        * **Maven**: pom.xml
        * **Gradle**: build.gradle, settings.gradle, etc.
    * **Go**: go.mod
---

**USING DOCKER CONTAINERIZATION OF PRODUCT-CATALOG SERVICE**

* Now create the Dockerfile
  
   ```
    FROM golang:1.22-alpine AS builder

    WORKDIR /usr/src/app
    
    COPY . .
    
    RUN go mod download
    
    RUN go build -o product-catalog ./
    
    FROM alpine AS release
    
    WORKDIR /usr/src/app
    
    COPY ./products ./products
    
    COPY  --from=builder  /usr/src/app/product-catalog ./
    
    EXPOSE ${PRODUCT_CATALOG_PORT}
    
    ENV PRODUCT_CATALOG_PORT 8088
    
    ENTRYPOINT ["./product-catalog"]
    ```
   
* Build the dockerfile using the command. This creates the image with the name `tulasipravallika/product-catalog:v1`
  
     `docker build -t tulasipravallika/product-catalog:v1 .`
   
* Check the image created using the command `docker images`.

* Execute/ Run the image using the command `docker run -it tulasipravallika/product-catalog:v1`. This gives the below output as mentioned in the README.md of the service.
  
    ```
    INFO[0000] Loaded 10 products                           
    INFO[0000] Product Catalog gRPC server started on port: 8088 
    ```
-----
**Note:** Execute the command `sudo usermod -aG docker ubuntu` followed by logout and log in/stop and start the docker if the permission denied error is triggered. 

-----

## Ad Service (Containerization)

### Steps

* Navigate to the `product-catalog` service folder
  ```
  cd ad/
  ```
  
* Read the `README.md` of the Ad service to confirm the build instructions.

---

**LOCAL EXECUTION**

  * Install jdk using the command `sudo apt install openjdk-21-jre-headless`
  * Follow the README.md and execute - `./gradlew installDist`. This command does the following :
    * Start the Gradle Daemon
    * Install the dependencies
    * Perform the compilation
    * Build the application
          
---

**USING DOCKER CONTAINERIZATION OF PRODUCT-CATALOG SERVICE**

* Dockerfile :

      ```
      FROM eclipse-temurin:21-jdk AS builder
      
      WORKDIR /usr/src/app/
      
      COPY gradlew* settings.gradle* build.gradle .
      
      COPY ./gradle ./gradle
      
      RUN chmod +x ./gradlew
      
      RUN ./gradlew
      
      RUN ./gradlew downloadRepos
      
      COPY . .
      
      COPY ./pb ./proto
      
      RUN chmod +x ./gradlew
      
      RUN ./gradlew installDist -PprotoSourceDir=./proto
      
      ########################################################
      
      FROM eclipse-temurin:21-jre AS release
      
      WORKDIR /usr/src/app/
      
      COPY --from=builder /usr/src/app ./
      
      ENV AD_PORT 9099
      
      EXPOSE ${AD_PORT}
      
      ENTRYPOINT ["./build/install/opentelemetry-demo-ad/bin/Ad"]
      ```
* Build the dockerfile using the command. This creates the image with the name `tulasipravallika/adservice:v1`
  
     `docker build -t tulasipravallika/adservice:v1 .`
   
* Check the image created using the command `docker images`.

* Execute/ Run the image using the command `docker run -it tulasipravallika/adservice:v1`. This gives the below output as mentioned in the README.md of the service.
  
  ```
  2025-11-21 06:23:09 - oteldemo.AdService - Ad service starting. trace_id= span_id= trace_flags= 
  SLF4J(W): No SLF4J providers were found.
  SLF4J(W): Defaulting to no-operation (NOP) logger implementation
  SLF4J(W): See https://www.slf4j.org/codes.html#noProviders for further details.
  2025-11-21 06:23:09 - oteldemo.AdService - Ad service started, listening on 9099 trace_id= span_id= trace_flags=
  ```


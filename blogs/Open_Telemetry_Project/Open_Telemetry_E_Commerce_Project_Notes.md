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

## Product Catalog Service (Containerization Target)

This repo contains ~20 microservices. For now, we will containerize only the **Product Catalog Service**.

---

### Steps

1. Navigate to the `product-catalog` service folder
  ```
  cd product-catalog/
  ```
  
2. Read its `README.md` to confirm the build instructions.
3. Run the commands below (as mentioned in that README):
  ```
  export PRODUCT_CATALOG_PORT=<any-unique-port>
  go build -o product-catalog .
  ```
---

##### Notes

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
4. For Go services, dependencies are automatically pulled during build.
    `go build -o product-catalog .`
     (-o specifies the name of the output binary. After the command runs successfully, a product-catalog binary is created in the current directory.)

5. To run the binary file.
    `./product-catalog ` - This executes the service and outputs the below lines as mentioned in the README.md of the service.
    ```
    INFO[0000] Loaded 10 products                           
    INFO[0000] Product Catalog gRPC server started on port: 8088 
    ```
6. Now create the Dockerfile
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
7. Build the dockerfile using the command. This creates the image with the name `tulasipravallika/product-catalog:v1`
     `docker build -t tulasipravallika/product-catalog:v1 .`
   
8. Check the image created using the command docker images. (**Note:** Execute the command `sudo usermod -aG docker ubuntu` followed by logout and log in/stop and start the docker if the permission denied error is triggered. )

9. Execute/ Run the image using the command `docker run -it tulasipravallika/product-catalog:v1`. This gives the below output as mentioned in the README.md of the service.
    ```
    INFO[0000] Loaded 10 products                           
    INFO[0000] Product Catalog gRPC server started on port: 8088 
    ```


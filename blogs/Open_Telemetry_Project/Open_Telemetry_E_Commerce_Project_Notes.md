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

* Navigate to the `product-catalog` service folder

  ```
  cd product-catalog/
  
  ```
  
* Read its `README.md` to confirm the build instructions.
* Run the commands below (as mentioned in that README):

  ```
  export PRODUCT_CATALOG_PORT=<any-unique-port>
  go build -o product-catalog .
  
  ```

---

### Notes

- Install `Go` if it’s not already installed:
  
  ```
  sudo apt install golang-go
  go version
  
  ```


- Dependencies vary by language and are usually defined in standard files:

- For Example
    * Python: requirements.txt
    * Java:
        * Maven: pom.xml
        * Gradle: build.gradle, settings.gradle, etc.
    * Go: go.mod

- For Go services, dependencies are automatically pulled during build.

  `go build -o product-catalog .` --> (-o specifies the name of the output binary. After the command runs successfully, a product-catalog binary is created in the current directory.)



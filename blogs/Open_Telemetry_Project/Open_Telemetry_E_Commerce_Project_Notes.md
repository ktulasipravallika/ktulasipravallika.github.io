
### Docker Installation

https://docs.docker.com/engine/install/ubuntu/#installation-methods


### Kubectl Install

https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/#install-kubectl-binary-with-curl-on-linux


### Terraform install

https://developer.hashicorp.com/terraform/install

### Open telemetery Project

https://github.com/ktulasipravallika/ultimate-devops-project-demo


### Clone the Project

git clone https://github.com/ktulasipravallika/ultimate-devops-project-demo.git
cd ultimate-devops-project-demo/src

##### PRODUCT CATALOG SERVICE

There are around 20 miicro services in this project. Let us just containerise product catalog service from this folder for now.

#### Steps

Go though README.md which usaully states the steps to build the application. In this case check out the README.md file of product-catalog service which states to execute the below commands.

```
export PRODUCT_CATALOG_PORT=<any-unique-port>
go build -o product-catalog . 
```

Note : Install `go` using command sudo apt install golang-go

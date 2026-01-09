### KUBERNETES

  * Kuberenetes is basically containers + networking + automation.

#### Image

  * A **container image** is a template / snapshot of a filesystem + metadata.
  * **Image** is a class / blueprint.
    * Example: nginx:1.27

#### Containers

  * A **container** is a running instance of an image.
  * A **container** is a running process on Linux that is isolated using:
    * namespaces (separate view of network, processes, etc.)
    * cgroups (resource limits: CPU/memory)
        * VM = full OS + kernel inside the VM
        * Container = shares host kernel, but isolated processes
  * **Container** is the object created from the image.

#### YAML

  * Indentation : YAML uses spaces (not tabs) to show nesting.
  * lists is represented as `- item`.
  * `key: value` is a map/dictionary.
  * `---` represents the multi-document YAML.
  * Lists of maps can be represented as below :
       ```
        containers:
          - name: web
            image: nginx:1.27
       ```
  * Number is represented as `replicas: 2`.
  * String is represented as `name: "2"`.
  
#### KUBECTL

 * kubectl is the command-line tool to talk to the Kubernetes API server.
    * Example : `kubectl apply -f file.yaml` 

#### CLUSTER

 * A cluster is a set of machines running Kubernetes.
 * It contains
    * Control Plane (brain)
    * Nodes (where workloads run)

#### Node

#### Commands





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

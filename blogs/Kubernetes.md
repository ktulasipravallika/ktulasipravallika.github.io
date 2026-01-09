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
 * A Kubernetes cluster is a complete system made of:
    * **Control Plane (brain) :** It consists of the below components.
      * **etcd:** Store the desired state.
      * **kube-apiserver:** Accept API requests.
      * **Scheduler:** Decide where Pods should run.
      * **Controllers:** Constantly fix things to match desired state.
 
    * **Nodes (where workloads run)**:
      * These are the “machines” where your applications actually run.
      * Each node runs:
         * **kubelet:** Agent that starts/stops Pods
         * **containerd:** Container Runtime
         * **Networking Components**

#### Node

#### Pod
* A **Pod** is a wrapper around one or more containers with shared networking and storage.
* A Pod is the smallest unit Kubernetes runs.
* A Pod usually contains one container (common case), but can contain multiple containers that share:
     * Same IP/network namespace
     * Same volumes
     * Same lifecycle

#### Deployments

* A Pod by itself is fragile and if it crashes or gets deleted, it’s gone.
* No built-in “keep 3 copies running and No rolling update control.
* A **Deployment** solves this by declaring:
   * “I want N replicas of this Pod template”.
   * Kubernetes continuously ensures N are running.
   * Supports rolling updates + rollback
* Deployment (you create this)
* ReplicaSet (Created/Managed by Deployment)
* Pods (Created/Managed by ReplicaSet)

#### Commands

* `kubectl apply -f file1.yaml`
  * `-f` → Indicates the file.
    
* `kubectl get pod pod_name`
  * kubectl get pod hello-pod -o wide → Adds extra columns (IP, Node, etc.)
  * kubectl get pod hello-pod -o yaml → Prints the full object YAML
  * kubectl get pod hello-pod -o json → Prints JSON
  * kubectl get pods -o name → Prints only resource names like pod/hello-pod
        { -o controls how kubectl prints the result. }
   
* `kubectl describe pod pod_name`
  
* `kubectl exec -it hello-pod -- ls`
  
* `kubectl port-forward pod/pod_name hostport:container_port`
  
* `kubectl delete -f file1.yaml`
  
* 





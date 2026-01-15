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
         * **kubelet:** Agent that starts/stops Pods.
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
* No built-in and No rolling update control.
* A **Deployment** solves this by declaring:
   * “I want N replicas of this Pod template”.
   * Kubernetes continuously ensures N are running.
   * Supports rolling updates + rollback
* Deployment (you create this)
* ReplicaSet (Created/Managed by Deployment)
* Pods (Created/Managed by ReplicaSet)

#### Commands

* `kubectl cluster-info`
* `kubectl get nodes`
* `kubectl version --client`
* `kubectl apply -f file1.yaml`
  * `-f` → Indicates the file.
    
* `kubectl get pod pod_name`
  
* `kubectl get deploy hello-deploy` → Shows details of deployment created.
  
* `kubectl get rs -l app=hello-deploy` → Shows details of replicaset created.
  
* `kubectl get pods -l app=hello-deploy -o wide` → Shows details of pod created.
  * `-l` → Fetches the information based on label.
  * `-o wide` → Adds extra columns (IP, Node, etc.)
  * `-o yaml` → Prints the full object YAML
  * `-o json` → Prints JSON
  * `-o name` → Prints only resource names like pod/hello-pod
  * `-o` controls how kubectl prints the result.

* `kubectl get all -A`
  
* `kubectl describe pod pod_name` → Describes the complete details of the pod including events.
  
* `kubectl exec -it hello-pod -- ls` → To enter into a pod and execute any commands.
  
* `kubectl port-forward pod/pod_name hostport:container_port` → This is to expose the port for the pod.

* `kubectl scale deploy hello-deploy --replicas=4`

* `kubectl set image deploy/hello-deploy web=nginx:1.26`
   * This updates the existing version of the image in the pods to a new version.
   * This happens as Rolling update ==i.e upgrade with zero/low downtime.
   * Kubernetes does NOT delete all pods at once, instead it:
       * Creates a new ReplicaSet (new version)
       * Gradually creates new pods from it
       * Gradually deletes old pods from the old ReplicaSet.
       * So traffic keeps working.
       * Rollback happens i.e Switch back to the previous ReplicaSet (previous working version).
         
* `kubectl rollout status deploy/hello-deploy`

* `kubectl rollout undo deploy/hello-deploy`

* `kubectl delete -f file1.yaml` → Deletes the yaml file.
  







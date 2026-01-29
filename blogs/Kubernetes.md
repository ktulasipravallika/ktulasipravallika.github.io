 ### KUBERNETES

  * Kuberenetes is basically containers + networking + automation.
  * Kubernetes is a Container Orchestration Platform (A manager for running containerized apps across machines).
  * Problemes Solved by Kuberenetes:
    * Single Host Dependency.
    * Auto Scaling of Containers.
    * Auto Healing of Containers.

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

#### Cluster

 * A cluster is a set of machines/ group of Nodes running Kubernetes.
 * A Kubernetes cluster is a complete system made of:
    * **Control Plane (brain) :**
      * It consists of the below components.
         * **etcd:**
             * Store the desired state.
             * This is a key-value storage for cluster related information.
         * **kube-apiserver:**
             * This is responsible for exposing the k8s to the external world.
             * Accept API requests.
         * **Scheduler:**
             * Decide where Pods should run.
             * Schedhules the pods/resources.
         * **Controller Manager:**
             * Constantly fix things to match desired state.
             * For example maintains the replicas count as mentioned in yaml and keeps track of it.
         * **Cloud Controller Manager:**
             * This is useful for interacting  with the cloud provider and creating/maintaining the resources with cloud.
 
    * **Data Plane / Nodes (where workloads run)**:
      * These are the “machines” where your applications actually run.
      * One master can have multiple worker nodes.
      * Each node runs:
         * **kubelet:**
             * This is responsible for creation/running/maintaining/start/stop the pods.
         * **Container Runtime:**
             * `containerd`, `Dockershim`, `cri-o` are examples of the container runtime.
             * This is responsible for running the containers in pod.
         * **Networking Components**
             * `kube-proxy` is responsible for the load balancing, networking, managing ip addresses.
             * It also uses iptables for networking on the machine.

#### Node

 *  A machine inside the cluster.
 *  In kind, nodes are Docker containers pretending to be machines.

#### Namespace

* A namespace is a folder/room to organize things.
* It prevents the objects from mixing.
  * Example: kube-system namespace holds Kubernetes internal components like DNS, networking, etc.
  * Analogy: Your house (cluster) has rooms (namespaces). Kitchen stuff shouldn’t be in the bedroom.

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
 * If a pod is updated directly, the ReplicaSet will just recreate it from the Deployment template.
 * Any “manual fix” on the pod is temporary and will be lost on restart/recreate.

#### Pod

 * A **Pod** is a wrapper around one or more containers with shared networking and storage.
 * A Pod is the smallest unit Kubernetes runs.
 * A Pod usually contains one container (common case), but can contain multiple containers that share:
      * Same IP/network namespace
      * Same volumes
      * Same lifecycle
 * Pods can die and be recreated.
 * A pod is like "one running instance of your app".

#### Containers

  * A **container** is a running instance of an image.
  * A **container** is a running process on Linux that is isolated using:
    * namespaces (separate view of network, processes, etc.)
    * cgroups (resource limits: CPU/memory)
        * VM = full OS + kernel inside the VM
        * Container = shares host kernel, but isolated processes
  * **Container** is the object created from the image.
  * Containers are ephemeral i.e Short Living.
    
#### Image

  * A **container image** is a template / snapshot of a filesystem + metadata.
  * **Image** is a class / blueprint.
    * Example: nginx:1.27
  
#### Service 

* A Service is a Kubernetes object that gives your pods a stable virtual IP + DNS name inside the cluster.
* Pods are temporary and change names/IPs when recreated.
* Service stays stable and routes traffic to the right pods.
* The Service load-balances across all matching pods.

#### Kind 
* `kind` is Kubernetes IN Docker.
* It creates a real Kubernetes cluster on your laptop using Docker containers as nodes.
* Perfect and Only used for learning and testing

#### Helm

* Helm is a package manager for Kubernetes.
* Instead of writing 20 YAML files manually, you do:
* Helm bundles all that into a chart (a reusable template package) and lets you configure with a values.yaml.

#### Commands

 * `kubectl cluster-info` → Gives the Cluster info in the current system. 

 * `kubectl version` → Gives the version of both server and client.
    * `kubectl version --client` → Gives the version of client.

 * `kubectl config set-context --current --namespace=namespace_name`
   
 * `kubectl get`
    * `kubectl get nodes` →  Give the list of nodes in the current cluster.  
    * `kubectl get pods` → Gives the list of pods in the default namespace.
    * `kubectl get svc` → Gives the list of services in the default namespace.
    * `kubectl get pods -l app=hello-deploy -o wide` → Shows details of pod created.
      * `-l` → Fetches the information based on label.
      * `-o wide` → Adds extra columns (IP, Node, etc.)
      * `-o yaml` → Prints the full object YAML
      * `-o json` → Prints JSON
      * `-o name` → Prints only resource names like pod/hello-pod
      * `-o` controls how kubectl prints the result. 
    * `kubectl get all -A`
      * `-A` is All namespaces.
      * It shows pods in every namespace not just “default”.
      * Without `-A`, Kubernetes shows only the current namespace (by default: default).
   * `kubectl -n deployment_name get pods` →`   
   * `kubectl get deploy deployment_name` → Shows details of deployment created.
   * `kubectl get rs -l app` →
   * `kubectl get ns`

 * `kubectl create ns namespace_name`
 
 * `kubectl -n namespace_name create deployment deployment_name --image=image_name` → Creates a Deployment with name and image mentioned.
 * `kubectl -n namespace_name expose deployment deployment_name --port=port_number` → Creates a Service pointing to pods managed by Deployment mentioned.
 * `kubectl -n namespace_name port-forward svc/web 8080:80` → Creates a temporary tunnel from the laptop to something in cluster {local port 8080 → remote port 80}

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
 *  * `kubectl apply -f file1.yaml` 
    * `-f` → Indicates the file.
  
 * `kubectl -n bootcamp set image deployment/deployment_name nginx=nginx:1.27`
 * `kubectl -n bootcamp delete deployment broken`


 * `kubectl delete -f file1.yaml` → Deletes the yaml file.
   
#### Kind Commands

* `kind create cluster --name cluster_name`
* 

 
#### Debugging

* **ImagePullBackOff** :
   * If the image: doesn’t exist or has a wrong tag or requires credentials (private registry) or the node can’t reach the registry (network/DNS), then the Pod can’t start and shows `ErrImagePull` first then `ImagePullBackOff`.
   * Kubernetes waits and retries with increasing delays = “backoff”
      * Example :
          * `kubectl -n bootcamp create deployment broken --image=nginx:doesnotexist`
             * Execute `kubectl -n bootcamp get pods`.
             * This gives an error `ImagePullBackOff or `ErrImagePull` 
   * **Debug Flow**
      * Check status → `kubectl -n namespace_name get pods`
      * Inspect details + events → `kubectl -n namespace_name describe pod pod_name`
        
* **CrashLoopBackOff** :
   * It means the container starts and quickly crashes.
   * Kubernetes tries to restart it and it keeps crashing.
   * Kubernetes starts delaying restarts (“backoff”).
   * This is usually caused by:
      * App error / bad config
      * Missing env var
      * Wrong command/args
      * App can’t reach dependency (DB)
      * Permission issues
    
  * **Pod stuck in Pending** :
    * A pod is Pending when it has not started running on any node yet.
    * That means Kubernetes couldn’t place it (schedule it) because something is missing, like:
      * Not enough CPU/memory on any node
      * Constraints don’t match any node (nodeSelector/affinity)
      * Required storage (PVC) not available
      * Taints/tolerations mismatch

**Note:**
* **Requests** → What the scheduler uses to place the pod.
* **Limits** → The maximum the container is allowed to use. (enforced by runtime)
  * If request is too high → Pod stays Pending
  * If limit is too low → app can get OOMKilled / throttled
* Requests affect scheduling and guaranteed resources; limits enforce the max usage at runtime.


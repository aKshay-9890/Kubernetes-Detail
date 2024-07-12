# Kubernetes-Detail

What is Kubernetes?
==> 
Kubernetes is an open-source Container Management tool that automates container deployment, container scaling, descaling, and container load balancing (also called a container orchestration tool).
Kubernetes is an open-source platform that manages Docker containers in the form of a cluster. Along with the automated deployment and scaling of containers, it provides healing by automatically 
restarting failed containers and rescheduling them when their hosts die. This capability improves the application’s availability.

Features of Kubernetes:
1.Automated Scheduling– Kubernetes provides an advanced scheduler to launch containers on cluster nodes. It performs resource optimization.
2.Self-Healing Capabilities– It provides rescheduling, replacing, and restarting the containers that are dead.
3.Automated Rollouts and Rollbacks– It supports rollouts and rollbacks for the desired state of the containerized application.
4.Horizontal Scaling and Load Balancing– Kubernetes can scale up and scale down the application as per the requirements.
5.Resource Utilization– Kubernetes provides resource utilization monitoring and optimization, ensuring containers are using their resources efficiently.
6.Support for multiple clouds and hybrid clouds– Kubernetes can be deployed on different cloud platforms and run containerized applications across multiple clouds.

/use/local/bin => contains all the binary and executable files.

# kubernetes Architecture:
In kubernetes architecture there is cluster. In cluster there are two planes as follows: 

# {1} Master Control Plane     
In master plane there are 4 components:
1. API-Server : It validates the request and authenticates the user.  It exposes the Kubernetes API, which allows users, administrators, and other components to communicate with the cluster.
2. Controller Manager : is used to monitor and make sure that every thing is working as we have define and will compare it with desire state
3. Scheduler :The Scheduler is responsible for placing Pods onto suitable worker nodes.  
4. etcd : it stores the metadata of all components.It holds the configuration data and the state of the entire cluster.

# {2} Worker Node Plane
1. Kubelet :  The Kubelet is an agent that runs on each worker node and communicates with the master control plane.The Kubelet works closely with the master control
   plane to start, stop, and manage containers based on Pod specifications.
2. kube-Proxy :  Kube Proxy sets up routing and load balancing so that applications can seamlessly communicate with each other and external resources.
3. Container runtime : A container runtime is the software responsible for running containers on the worker nodes.

# Difference between pod,container and deployment.
# Feature	                   Pod	                                                    Container	                                                      Deployment
Definition     The smallest deployable unit in Kubernetes	             A lightweight, standalone, and executable software package      	An abstraction to manage Pods and their updates
Purpose	      Encapsulates one or more containers to run together	    Runs a single application or service with dependencies	         Manages the rollout and scaling of multiple Pods
Lifecycle	   Managed by Kubernetes                                	    Managed by the Pod	                                             Managed by the Deployment
Isolation	   Shares resources and network with containers inside it    Isolated process within a Pod                                	   Groups and manages multiple Pods
Networking	   Has a unique IP address within the cluster	             Shares the network namespace of the Pod	                        Configures the networking for its Pods
Scaling	      Scaled by creating or deleting Pods	                      Cannot be scaled independently	                                 Handles scaling of Pods automatically
Updates	      Requires recreation of the Pod                            Updated by replacing the Pod	                                    Supports rolling updates and rollbacks

# Difference between deployment and replicaset.
# Feature	                            Deployment                                                              	ReplicaSet
Definition	            Manages a set of Pods, providing updates and rollback capabilities	     Ensures a specified number of Pod replicas are running at any given time
Purpose	               To manage the lifecycle, updates, and scaling of applications	           To maintain a stable set of replica Pods running
Lifecycle Management   	Handles rolling updates, rollbacks, and history tracking	                 Does not manage rolling updates or rollbacks
Updates	               Supports rolling updates and rollbacks                                    Does not support rolling updates or rollbacks
Declarative State	      Manages desired state through Deployment configuration	                 Ensures desired number of replicas as specified
Use Cases	            When you need advanced deployment strategies like rolling updates	        When you simply need to maintain a specific number of replicas
Configuration	         Defined by a Deployment manifest in YAML	                                Defined by a ReplicaSet manifest in YAML

# Difference between imperative and declarative approach.
# Feature                                  	Imperative Approach	                                          Declarative Approach
Definition                 Specifies the exact steps to achieve a desired state	          Specifies the desired end state without detailing the steps to achieve it
Method	                  Commands executed sequentially to perform tasks           	    Defines the desired state in configuration files or manifests
Complexity                 Can become complex with many steps	                            Simplifies management by focusing on the end state
Flexibility	               Offers fine-grained control over each step	                   Higher-level abstraction, less control over individual steps
Usage Example           	Using kubectl run to create Pods directly	                      Using kubectl apply with a YAML file to define resources
Reproducibility            Harder to reproduce due to manual steps	                      Easier to reproduce as the desired state is defined in code
State Management           No built-in state management, state changes are manual	       Kubernetes manages the state and ensures it matches the desired configuration
Automation	               Less suitable for automation due to step-by-step nature	       Well-suited for automation and CI/CD pipelines
Error Handling	            Errors need to be handled at each step	                         Kubernetes handles discrepancies and attempts to reach the desired state
Scalability	               Manual scaling requires explicit commands	                      Declarative scaling through configuration files
Examples in Kubernetes    	kubectl create, kubectl delete, kubectl scale	                kubectl apply, kubectl delete -f, kubectl diff

# Declarative: In this method we write yaml/manifest file and then do the changes. Here if we want to add labels then we add it in yaml file.
# Imperative: By using direct commands i.e. if we want to attach labels to pod by using command we can do it directly

# Pod recreating mechanism is called as Auto Healing
In deployment we decide how many pods can be in worker node

# Why kubernetes is required?
=> Kubernetes does auto healing and auto scaling.
   Auto Healing contains Deployment and replicaset. Uses labels and selector method.
   Replica decides how many pods can contain in node.

# Services : In Kubernetes, a Service is a method for exposing a network application that is running as one or more Pods in your cluster.
  1. Load balancing 
  2. Service Discovery
  3. Exposing to world
   
# what is yaml? 
=> yet another markup language

In terms of kubernetes pod is a yamal manifest
watch -n 2 kubectl get pod  (to see the pod)

commands :-
-kubectl get all    (shows all resources) 
-kubectl get all -A
-kubectl get namespaces  
   There are default 4 namespaces:
    default
    kube-node-lease
    kube-public
    kube-system
-
-kubectl get namespaces
-kubectl get pods -n <namespaces>
# To create namespaces:
kubectl create namespace -n CDECB
vim mynamespace.yml

kubectl create -f mynamespace.yml

vim pod.yml
kubectl create -f pod.yml

kubectl get po  
kubectl describe po nginx

# To see yml file of pod : 
kubctl get po
kubectl get po <"pod-name"> -o yml

# Kubernetes service is a service which provide a static IP to pod .
 # Service Types:
1. Load Balancer service: using labels and selectors, service will expose applicatio onto external world.
2. Node Port Service : those who have access to worker node/ VPC /Instance i.e inside organization (port range 30,000 - 32 ,767).
3. Cluster IP Service : Application will access only inside the kubernetes cluster. (by default)
 4. Externalname service : use to map 

# Taints and toleration:
- Taints and Toleration work together to ensure that pods are not schedule onto inappropriate nodes.
- One or more Taints are applied to a node, this mark that node should not accept any other pod that do not tolerate taints.
- Taints are applied to nodes and tolerants are applied to pods.
- Taint Effect Types:
-    1. NoSchedule --> The pod will not get scheduled to the node without a matching toleration.
     2. Prefer NoSchedule --> This is a softer version of NoSchedule where the controller will not try to schedule a pod with the tainted node. However, it is not a strict requirement.
     3. NoExecute -->  This will immediately evict all the pods without the matching toleration from the node.

# Labels and Selectors
 Labels are the mechanism you use to organise kubernetes objects. A label is a key-value pair without any predefined meaning that can be attached to the object (Pod / Node). Multiple labels can be added to pods.
 Selectors are used to identify group of objects.
  Command To add label to an existing pod :
    ==> kubectl label pods <pod-name> <key>=<value>
    To show labels:
    ==> kubectl get pods --shoe-labels
    to list pods matching labels 
    ==> kubectl get pods -l <key>=<value>
    to delete pod using labels
    ==> kubectl delete pod -l <key>=<value>

# Rollback and Rollout
==> A rolling update allows you to deploy a newer version of an application (such as bug fixes, minor features, or enhancements) without causing downtime.
Here’s how it works: A new ReplicaSet is created, and the Deployment manages moving Pods from the old ReplicaSet to the new one at a controlled rate.
Commands for rollout:
kubectl create deploy nginx-deploy --image=nginx:1.14.1
kubectl get deploy   (to see rollout)
kubectl set image deployment/<deployment-name> nginx=nginx:1.16.1 --record=true  (to change version and save command)
kubectl rollout status deployment/<deployment-name>  (To check status)
    kubectl rollout status deployment/nginx-deployment
   kubectl rollout history deployment/nginx-deployment  --revision=<revision no.> (To check history & of particular version)
   kubectl rollout undo deployment/nginx-deployment  (To undo the latest rollout)
   kubectl rollout undo deployment/<deployment-name> --to-revision=<revision-number>   (Rollout to previous versions)

==> Rollback is the ability to revert back to an older working version of an application in case something goes wrong.
For example, if a new deployment causes issues, you can use the kubectl rollout undo command to revert to the previous known state.

# Command and Arguments
# Environment Variable
# Configmap and secrets

What is the difference between configmap and secrets ? 

Feature                  	ConfigMap	                                                         Secret
Purpose          	   Store non-sensitive configuration data	                  Store sensitive data, such as passwords and tokens
Data Encoding	      Plaintext (base64-encoded when stored in etcd)	         Base64-encoded (and encrypted at rest in etcd)
Use Case Examples    Application configuration, environment variables	      Passwords, API keys, certificates
Data Limit   	      Large, up to 1MB	                                       Smaller, recommended to keep it within a few KB
Security            	Not encrypted, only base64-encoded	                     Encrypted at rest and more secure
Access Control	      Managed by Kubernetes RBAC	                              Managed by Kubernetes RBAC
Access from Pods	   Mounted as volumes or used as environment variables	   Mounted as volumes or used as environment variables
Creation            	kubectl create configmap	                              kubectl create secret

# What is difference statefullset and deployment ?
Feature	                        StatefulSet	                                         Deployment
Purpose              	Manages stateful applications                     	    Manages stateless applications
Pod Identity        	   Each Pod has a unique, stable network identity	       Pods are interchangeable
Pod Names	            Pods are named with a predictable ordinal suffix	    Pod names are generated randomly
Persistent Storage	   Supports persistent storage with unique volumes      	 Can use persistent storage, but volumes are not unique
Scaling	               Maintains the order of deployment and scaling	       Scales up or down randomly
Update Strategy	      Rolling updates with ordered guarantees	             Rolling updates without ordering guarantees
Network Identity	      Each Pod gets a stable network identity (DNS)	       Pods share the same network identity
Use Case Examples     	Databases, Kafka, Zookeeper	                         Web servers, microservices, batch jobs

# Statefullset : In Kubernetes, a StatefulSet is a workload API object used to manage stateful applications. It provides unique guarantees about the ordering and uniqueness of Pods, which is particularly useful for stateful applications where each instance needs persistent storage and stable network identities.

# Persistent Volume & Persistent Volume Claim and their access mode. PV & PVC

==>> To manage statefull application we use statefulset

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

kubernetes Architecture:
In kubernetes architecture there is cluster. In cluster there are two planes as follows: 

{1} Master Control Plane     
In master plane there are 4 components:
1. API-Server : It validates the request and authenticates the user.  It exposes the Kubernetes API, which allows users, administrators, and other components to communicate with the cluster.
2. Controller Manager : is used to monitor and make sure that every thing is working as we have define and will compare it with desire state
3. Scheduler :The Scheduler is responsible for placing Pods onto suitable worker nodes. 
4. etcd : it stores the metadata of all components.It holds the configuration data and the state of the entire cluster.

{2} Worker Node Plane
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


# what is yaml? 
=> yet another markup language

In terms of kubernetes pod is a yamal manifest

commands :-
-kubectl get all    (shows all services) 
-kubectl get namespaces  
   There are default 4 namespaces:
    default
    kube-node-lease
    kube-public
    kube-system
-
-kubectl get namespaces
-kubectl get pods -n <namespaces>
To create namespaces:
kubectl create namespace -n CDECB
vim mynamespace.yml

kubectl create -f mynamespace.yml

vim pod.yml
kubectl create -f pod.yml

kubectl get po  
kubectl describe po nginx

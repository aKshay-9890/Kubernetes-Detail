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





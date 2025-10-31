# Kubernetes
Day - 01
What are the features that docker can't solve?

The major areas that docker can't achieve are

The docker is a single host: the meaning of single host is that it is installed and can create containers in a single host.

Auto healing:
let's take an organization project where we will have many containers with microservices running. It's not always easy to check the status of the container by using the command docker ps.
We need auto healing so that the containers will be up and running.

Auto scaling: the application should be able to scale automatically there are 2 ways to scale
One way is by creating the containers that can balance the load when it receives more user requests.
Example: let's take a real time example of an ott platform.
Most of the times the requests or the users accessing that application are 100 members if suddenly on some weekends or on any other holidays it may receive 10x.
Now it should be able to handle this which is not possible in the containers.

Lack of Enterprise level standards:
An application will be considered as an enterprise level application if it comes with the standards load balancer, firewall, auto scaling and healing.
The list is will go further but these are the most important among them.
Unfortunately, the docker is not capable of this until unless we use some tools or platforms like docker swarm.

Also, these are the main differences between the docker and Kubernetes.
The most important thing about k8s is this is a container orchestration tool.

How will Kubernetes solve these problems?
There were couple of disadvantages of the docker now how they were solved
First problem is single host:
As we know that the Kubernetes is by default a cluster means group of nodes it will be installed in a master node.
Can't we install it in a single node, yes we can but we can just practice or can be installed in a developer environment which is not possible in the production.
The problem with this single host is that if a container is not having enough resources because of the other containers that are present in the host then that container will be killed.
Whereas in the k8s in this scenario the container that have the less resources will be moved to the another node so that it will or the application in that container will be alive.

Second problem: Auto scaling
Now in k8s there are 2 ways to autoscale.
There is a file called replication controller yaml file of replica set in which manually can write the replica set from 1 to 10.
This will scale up the application automatically when it receives multiple requests.
Second way: there is a feature called horizontal pod auto scaler(HPA) this feature will automatically spin up the creation of the container whenever we need to scale.

Auto healing:
Now when a container goes down, the application or the user will not be able to access the service.
To overcome this k8s have a API server which will roll out a container even before the container goes down so that it can able to be up even if the container goes down.

The enterprise level standards:
The k8s will have all the necessary standards that are needed for an application.


This k8s is a part of the borg which is not open source running by the google but the k8s is part of that borg which comes with the enterprise level container orchestration platform.
We can't say that the Kubernetes is 100% still there are some challenges which are being developed a community of people to make it happen.

Day-02


Kubernetes Architecture
Kubernetes is mainly divided into two parts: Control Plane (or Master Node) and Data Plane (or Worker Node).

Control Plane
The Control Plane consists of key components responsible for cluster management and control actions.

The first and most important one is the API Server, which is often called the heart of the Kubernetes cluster. It handles requests from various sources such as kubectl, users, and internal cluster components.

Next is the Scheduler, which is responsible for allocating resources and scheduling workloads onto the appropriate worker nodes. When multiple worker nodes are available, the Scheduler determines which node should execute a given pod.

Another essential component is etcd, a distributed key-value store that holds the entire cluster’s state and configuration data.

The Controller Manager is also part of the Control Plane. It manages various controllers that handle cluster operations such as auto-healing, auto-scaling, and load balancing.

Data Plane (Worker Node)
In the cluster, the smallest deployable unit is a Pod, which acts as a wrapper around one or more containers.
To run containers, Kubernetes uses a container runtime, which is responsible for executing and managing containerized applications.

One major advantage of Kubernetes is its auto-healing feature, powered by the Kubelet component present on each worker node. Kubelet ensures that pods are running as expected; if any issue occurs, it reports to the API Server in the Control Plane, which handles recovery or rescheduling.

Another important component is Kube-Proxy, which manages network communication and load balancing across pods. It is responsible for service networking, assigning IP addresses, and ensuring requests are properly routed to different pods through mechanisms like ReplicaSets when scaling is needed.


Day 03:
  docker run hello-world
Tests if Docker is correctly installed and running.

  sudo apt install -y apt-transport-https ca-certificates curl
Allows secure downloads over HTTPS and adds tools like curl for fetching files.

  curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
Ensures downloaded Kubernetes packages are verified and trusted.

  echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
Adds the official Kubernetes package source to the system.

  sudo snap install kubectl --classic
installs kubectl, the Kubernetes CLI used to control and manage clusters.

  kubectl version --client
Confirms that kubectl is installed and displays client version details.

  curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
Downloads the latest stable Minikube binary for Linux.

  sudo install minikube-linux-amd64 /usr/local/bin/minikube
Moves the Minikube binary to a system path, making it accessible globally.

  minikube version
Verifies that Minikube was successfully installed.

  minikube start --driver=docker
Initializes a local Kubernetes cluster using Docker as the virtualization driver.

  minikube status
Displays the current state of the Minikube cluster components.

  kubectl cluster-info
Shows cluster details such as API server and DNS info.

  kubectl config view
Displays kubeconfig details like context, users, and cluster settings.

  kubectl get nodes
Lists all active nodes in your cluster (usually one node in Minikube).

  kubectl get deployment
Displays all deployed applications and their current state.

  kubectl get pods
Lists all pods (containers) running in the cluster.

  kubectl get services
Lists Kubernetes services that expose your pods to internal or external traffic.

  minikube service my-nginx
Opens the exposed service (e.g., Nginx) in your web browser via Minikube tunnel.

Docker, kubectl, and Minikube successfully installed and configured.
Local Kubernetes cluster running using Docker driver.
Verified nodes, pods, and services accessible through kubectl and Minikube.

Docker	Container runtime	docker run hello-world
kubectl	Kubernetes CLI	kubectl version --client
Minikube	Local Kubernetes cluster	minikube version / minikube start

Day - 03

The other day I have installed the minikube and kubectl where this minikube is a local environment to create and manage the clusters.
And kubectl is where it manages this local environment by communication with the clusters.

But with this miikube we can just practice kubernetes where it is actually not been used in the real production.
Also we have other tools like microk8s like minikube
Now to manage the create the clusters and manage them in the real world we have platforms Kubernetes, Openshift, Rancher and like EKS, GKE, and AKS which are used in the real production.

Here also this self managed Kubernetes has been used most of the time until unless there is critical situation  they use managed solutions like EKS.

There is a popular one which is widely used is kops-Kubernetes operations.
This will automate the lifecycle of Kubernetes like creating, running, deleting and all the other tasks.
This kops will reduce the manual way of maintaining or managing the clusters.
The configurations are stores in s3 bucket which helps in reproducibility and management.

We need to configure AWS Cli and permissions like EC2 and S3.
We need to create a S3 bucket to store the state of the cluster.
Then need  to use the kops to create the cluster by specifying the name region node count.
After which we will use a real time DNS domain or can be a local domain.
Finally need to finalize the cluster with the kops commands and then need to aware of the charges.

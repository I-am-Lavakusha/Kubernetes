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

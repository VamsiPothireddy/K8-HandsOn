**Why Services is Needed?**



When we have a deployment object in place, we can achieve autohealing (specifying a number of replicas, and a replicaset ensures that the specified number of replicas in the deployment will be available).

Let's say, for some reason, a pod dies and another pod is created with a new IP address. Obviously, we need to know the new IP address to access it. By adding a service component, this can be achieved—how? Service, instead of keeping track of IP addresses created/destroyed, keeps track using labels and selectors mentioned in the deployment file. If any pod with the same label is created with a different IP, the service routes traffic to that IP. This is nothing but the discovery of pods using service.

Next, it load balances traffic to multiple pods using the kube-proxy component.

Exposing to the outside world: Let's say if there is no service, then we get multiple IP addresses for each pod and we need to SSH into the worker node where the pod is running to access them. But service provides functionality of exposing to the public using three different approaches.

Cluster IP
Node Port
Load balancer
Cluster IP is by default; we need to get into the worker node and access it.
Node port, if we have access to the worker node we can access.
Load balancing, this usually gives a public IP address where anyone in the world can access using the public IP address, but this can be achieved using EKS/AKS/some cloud provider. For example, if we go with EKS, the cloud control manager in K8s helps in creating a public IP with ELB (Elastic Load Balancer) for the public to access.

If we want to get capabiities of nodeport and load balancer always start minikube with hyperkit supervisor by default if we dont specify it runs with docker which gives only limited features 

minikube start --memory=4096 --driver=hyperkit

![K8s-4](https://github.com/VamsiPothireddy/K8-HandsOn/assets/47288461/9f8feeb4-0e56-48bf-b735-f985da7999b1)
<img width="1440" alt="Screen Shot 2024-05-14 at 7 33 27 AM 1" src="https://github.com/VamsiPothireddy/K8-HandsOn/assets/47288461/adb69836-6a12-4835-9fc9-f1fa8503bd3f">
<img width="1440" alt="Screen Shot 2024-05-14 at 12 52 02 PM" src="https://github.com/VamsiPothireddy/K8-HandsOn/assets/47288461/127737ff-319c-42c2-8ab6-f7b04fb70032">
<img width="814" alt="Screen Shot 2024-05-14 at 3 05 47 PM" src="https://github.com/VamsiPothireddy/K8-HandsOn/assets/47288461/4de45c21-9af7-46f3-8c5c-7922b9f1d5a1">



**Why Services is Needed?**

When we have deployment object  using whcih we can achive autohealing (specifcy number of replicas and replicaset  makes sure mumber of replcias specified in deployment will be available)

Lets say for some reason pod died and another pod created with new IP address , obviosuly we need one needs to know new IP address to access , by adding service componnet this can be achived - how ? Service instead of keep tracks of IP addresses created /detroyed its keeps track uinsg lables and selectors mentioned in deployment file . If any pod with that same label created with different IP service routes traffic to that IP. This is nothing but discovery of pods using service.

Next it load balances traffic to multiple pods using kube-proxy componnet. 

Exposiing to outside world : Lets say if there is no service , then we get mutiple IP addresses for each pod and we need to ssh into worker node where pod is running and access them , but service provides funcatnality of exposing to public using 3 different approaches . 

1) Cluster IP
2) Node Port 
3) Load balancer 

Clsuter IP is by default , we need to get int to worker node and acesss                                                          
Node port , if we have access to worker node we can access                                                                       
Load balancing , this usally gives public IP address where anyone in world can access using public IP address , but this can be achived using EKS/AKS / some cloud provider .ex : if we go with EKS , cloud control manager in K8s helps creating public IP with ELB (Elastic load balancier) for public to access.



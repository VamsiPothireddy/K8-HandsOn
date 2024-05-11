## Architecture 

<img width="725" alt="image" src="https://github.com/VamsiPothireddy/K8-HandsOn/assets/47288461/17a7a70b-169f-42cb-8565-467c118a18d4">


### Comparison with Docker and how it addresses limitations

Single Node problem: Can be addressed using cluster Architecture. Here we are showing a simplified version where one master and one worker node. In production, usually, a cluster consists of multiple master and worker nodes.

Master node components are referred to as Control plane components, and worker node components are referred to as data plane components.

Auto Healing: Kubelet in the data plane ensures pods are running. If not, it informs the API server, and the API server instructs the scheduler to spin up a pod. etcd is a backup or metadata of the whole cluster, which stores information in a key-value structure. Using this data, the API server informs the scheduler on which worker node a pod has to spin up (if multiple worker nodes exist).

Auto Scaling: In Kubernetes, there are controllers like ReplicaSet where we can specify the number of pods or HPA (Horizontal Pod Autoscaling) so based on load, pods can spin up. We can mention max/min pods. These controllers are managed by the Control Manager in the control plane. Since Kubernetes can be cloud-specific like EKS, AKS, etc., an interface called cloud control manager is provided to have cloud-specific implementation given by the cloud provider. For example, AWS gives EKS Cloud Control Manager, Azure provides for AKS.

Just as we need JAVA software to run Java applications, similarly, we need a container runtime to run containers. In Docker, it's dockershim; similarly, in Kubernetes, we can use either dockershim, CRI-O, or containerD.

In Docker, there's a default network bridge that assigns IP addresses for each container; similarly, kube-proxy takes care of networking, like assigning addresses and also acts as a basic load balancer. For example, if two pods are present, it routes traffic to both pods.

### What is Kubernetes and why do we need it?
Kubernetes is a container orchestration platform which addresses the limitations of just using containers alone. Docker Swarm is another orchestration solution, but Kubernetes offers more features. Let's examine the limitations first. I'm referring to Docker as the container platform and Kubernetes as the orchestration platform.

**Limitations Of Container platforms (Docker)  **

Single Node: By default, Docker installs on a single node (which may be a physical machine or EC2 instance) and runs containers on top of it. This creates a single point of failure. Kubernetes addresses this using a master node architecture where multiple machines (EC2 instances or physical bare metal boxes) form a cluster.

Autohealing: If any container goes down, without an orchestration platform, we need to manually spin up the container again. Also, verifying if any container is going down is not practical. Kubernetes solves this problem with features like Horizontal Pod Autoscaler (HPA), which automates the scaling of containers.

Autoscaling: Increasing containers based on load can be achieved with Kubernetes.

Meeting enterprise standards such as load balancing, whitelisting, blacklisting, etc., can all be achieved through Kubernetes.

Kubernetes not only provides out-of-the-box solutions, but also offers flexibility to create custom functionality using custom resources. For example, Kubernetes provides load balancing by default, but using the Ingress Controller concept, we can achieve advanced load balancing by integrating with tools like F5 or Nginx.
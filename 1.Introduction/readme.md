### What is Kubernetees and why we need it ? 

Its an container orchestration platoforms which solves limitation of just contaiers . Docker swarm is another orchestration solution but K8 gives more features . Lets see the limitation first. Im refering doccker as contaier platoform and K8 as orchestration platoform.

**Limitations**

Single Node : By default docker installs on single node (may be phusycal machine/ EC2) and runs containers on top of it . Which is single point failure . K8 address this using master node architecture where mutiple machines (EC2s or physical bare metal boxes) forms cluster

Autohealing: If any container goes down , without orchestration platfrom , we need to again spinup comatiner manually . Also need to verify if any container is going down - this is not practical- K8 solves this problem features like hpa (auto scaling concept)

Autoscaling: increase containers based on load ,this can be achieved with K8

Not meeting enterprise standards like ,load balancing , white listing , block listing etc . All these can be achived throgh k8.

K8 does not only provides out of box silution , but we have flexibility to create custom functioncality using custom resources. Ex: K8 by default provides out of box load balanacing but using ingress controller conceprt we can achieve advanced level of load balancing by integrating with tools like F5 or ngnix

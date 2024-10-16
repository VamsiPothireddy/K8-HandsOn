Creating EKS Cluster with two worker nodes
eksctl create cluster   --name demo-cluster   --region us-east-1   --nodegroup-name standard-workers   --node-type t3.small   --nodes 2   --nodes-min 2   --nodes-max 2   --managed   --node-private-networking   --ssh-access   --ssh-public-key BastionServerKeyPair

aws eks update-kubeconfig --name demo-cluster

scp -i /Users/Vamsi/BastionServerKeyPair.pem /Users/Vamsi/BastionServerKeyPair.pem ec2-user@ec2-35-172-121-69.compute-1.amazonaws.com:/home/ec2-user/


ssh -i "BastionServerKeyPair.pem" ec2-user@ec2-35-172-121-69.compute-1.amazonaws.com


curl http://192.168.78.10:32493

curl http://192.168.115.235:32493


Tejas-MacBook-Pro:~ Vamsi$ kubectl get nodes
NAME                              STATUS   ROLES    AGE   VERSION
ip-192-168-115-235.ec2.internal   Ready    <none>   80m   v1.25.16-eks-f479e3c
ip-192-168-78-10.ec2.internal     Ready    <none>   80m   v1.25.16-eks-f479e3c
Tejas-MacBook-Pro:~ Vamsi$ 



kubectl get pods -n game-2048 -o wide
NAME                               READY   STATUS    RESTARTS   AGE   IP                NODE                              NOMINATED NODE   READINESS GATES
deployment-2048-5686bb4958-dmfh7   1/1     Running   0          39m   192.168.103.192   ip-192-168-115-235.ec2.internal   <none>           <none>
deployment-2048-5686bb4958-f89z7   1/1     Running   0          39m   192.168.82.158    ip-192-168-78-10.ec2.internal     <none>           <none>
deployment-2048-5686bb4958-p28lp   1/1     Running   0          39m   192.168.116.232   ip-192-168-115-235.ec2.internal   <none>           <none>
deployment-2048-5686bb4958-rn4w9   1/1     Running   0          39m   192.168.88.71     ip-192-168-78-10.ec2.internal     <none>           <none>
deployment-2048-5686bb4958-xrl2k   1/1     Running   0          39m   192.168.65.230    ip-192-168-78-10.ec2.internal     <none>           <none>

![Screen Shot 2024-10-12 at 9 46 56 PM](https://github.com/user-attachments/assets/2a8ba041-0ac1-4bcc-b44f-39cd91815dcb)
![Screen Shot 2024-10-12 at 8 26 27 AM](https://github.com/user-attachments/assets/bb80c394-4769-4211-8fa8-fe331f924c0e)

Load balancer is nothing but pod runnin on cluster , and its ingress controller . Unless we install ingress controller ,ingress is of no use. This keeps checking ingress resources and exposes ttraffic to outside world and also creates AWS resource called ALB(Application Load Balancer)

Since pod has to create AWS resource, it should (service account associated with pod) have some level of permissions , thats why we are creating AWSLoadBalancerControllerIAMPolicy  , attach policy to AmazonEKSLoadBalancerControllerRole . Once role gets created we map this role to Service account of pod(aws-load-balancer-controller --this is pod name)

Creating Policy: 
curl -O https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/v2.5.4/docs/install/iam_policy.json

aws iam create-policy \
    --policy-name AWSLoadBalancerControllerIAMPolicy \
    --policy-document file://iam_policy.json

Creating IAM role and attaching Policy:

eksctl create iamserviceaccount \
  --cluster=demo-cluster \
  --namespace=kube-system \
  --name=aws-load-balancer-controller \
  --role-name AmazonEKSLoadBalancerControllerRole \
  --attach-policy-arn=arn:aws:iam::805179198157:policy/AWSLoadBalancerControllerIAMPolicy \
  --approve

  Above command created IAM role named : AmazonEKSLoadBalancerControllerRole and atatched AWSLoadBalancerControllerIAMPolicy . It also created service account in EKS cluster named: aws-load-balancer-controller and annotated with IAM role. Now ALB controller uses this service account indirectly uses IAM role to interact with AWS resources , in this case interacts with ALB creation service and creates ALB controller.

  Now lets install ingress controller  here type of ingress controller is AWSALBController, it can be any like ngnix ingress controller

  Since we dont want to manually write deployment file to created ALB controller pod , im using helmchart and pass inout varaibales to create my ALBController , deployment and pods

  helm repo add eks https://aws.github.io/eks-charts
  helm repo update eks

 helm install aws-load-balancer-controller eks/aws-load-balancer-controller \
  -n kube-system \
  --set clusterName=demo-cluster \
  --set serviceAccount.create=false \
  --set serviceAccount.name=aws-load-balancer-controller \
  --set region=us-east-1 \
  --set vpcId=vpc-0b67bdbdb4df04133

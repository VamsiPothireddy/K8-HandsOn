**Skeleton of Kubeconfig file**

usullay located under user folder ~/.kube/config

It has 3 section Clusters,Contexts,Users
Below file has configured with two clusters , one with minkube runnung locally and another is aws managed cluster eks

Context here is mapping between Users and Cluster. Here Minikube user has mapped to minikube cluster and user name called 'arn:aws:eks:us-east-2:<AWSAcciountNumber>:cluster/test-cluster' mapped to 'arn:aws:eks:us-east-2:<AWSAcciountNumber>:cluster/test-cluster' cluster



apiVersion: v1
kind: Config
clusters:
- cluster:
    certificate-authority-data: XxxxxxxxxxxxXxxxxxxxxx
    server: https://5XXXXXXXXXXXXXXX.gr7.us-east-2.eks.amazonaws.com
  name: arn:aws:eks:us-east-2:<AWSAcciountNumber>:cluster/test-cluster
- cluster:
    certificate-authority: /Users/Vamsi/.minikube/ca.crt
    extensions:
    - extension:
        last-update: Thu, 25 Apr 2024 07:14:23 EDT
        provider: minikube.sigs.k8s.io
        version: v1.32.0
      name: cluster_info
    server: https://127.0.0.1:51971
  name: minikube
contexts:
- context:
    cluster: arn:aws:eks:us-east-2:<AWSAcciountNumber>:cluster/test-cluster
    user: arn:aws:eks:us-east-2:<AWSAcciountNumber>:cluster/test-cluster
  name: arn:aws:eks:us-east-2:<AWSAcciountNumber>:cluster/test-cluster
- context:
    cluster: minikube
    extensions:
    - extension:
        last-update: Thu, 25 Apr 2024 07:14:23 EDT
        provider: minikube.sigs.k8s.io
        version: v1.32.0
      name: context_info
    namespace: default
    user: minikube
  name: minikube
current-context: minikube
users:
- name: arn:aws:eks:us-east-2:<AWSAcciountNumber>:cluster/test-cluster
  user:
    exec:
      apiVersion: client.authentication.k8s.io/v1alpha1
      args:
      - --region
      - us-east-2
      - eks
      - get-token
      - --cluster-name
      - test-cluster
      command: aws
      env: null
      interactiveMode: IfAvailable
      provideClusterInfo: false
- name: minikube
  user:
    client-certificate: /Users/Vamsi/.minikube/profiles/minikube/client.crt
    client-key: /Users/Vamsi/.minikube/profiles/minikube/client.key






**Adding Users to Minikube cluster**


K8 Authnentication Mechanism:
When K8 is created , it comes with its own prublic and private key pair . All authentications are taken care using this set of files.

Describe kube-apiserver pod in kube-system name space to see cert and key file locations of K8 clsuter.
kube-apiserver-minikube

kubectl describe pod kube-apiserver-minikube -n kube-system. Look for cert and key file location 


 --client-ca-file=/var/lib/minikube/certs/ca.crt




Generate private key and CSR (Certficate Signing Request ) using any tool and Sign CSR using K8's puboic cert whiich gives pubcert file for user . 


Add user's public key and priviate key to kubeconfig file. 

generate private key & CSR
openssl genrsa -out devuser.key 2048 
openssl req -new -key devuser.key -out devuser.csr -subj "/CN=devuser/O=developers"




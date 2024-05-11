**Skeleton of Kubeconfig file**

usullay located under user folder ~/.kube/config

It has 3 section Clusters,Contexts,Users
Below file has configured with two clusters , one with minkube runnung locally and another is aws managed cluster eks

Context here is mapping between Users and Cluster. Here Minikube user has mapped to minikube cluster and user name called 'arn:aws:eks:us-east-2:<AWSAcciountNumber>:cluster/test-cluster' mapped to 'arn:aws:eks:us-east-2:<AWSAcciountNumber>:cluster/test-cluster' cluste





**Adding Users to Minikube cluster**


K8 Authnentication Mechanism:
When K8 is created , it comes with its own prublic and private key pair . All authentications are taken care using this set of files.

Describe kube-apiserver pod in kube-system name space to see cert and key file locations of K8 clsuter.
kube-apiserver-minikube

kubectl describe pod kube-apiserver-minikube -n kube-system. Look for cert and key file location 


 --client-ca-file=/var/lib/minikube/certs/ca.crt




Generate private key and CSR (Certficate Signing Request ) using any tool and Sign CSR using K8's public cert & private key whiich gives pubcert file for user . 
Add user's public key and priviate key to kubeconfig file. 

**Commands to generate private key & CSR**
openssl genrsa -out devuser.key 2048 
openssl req -new -key devuser.key -out devuser.csr -subj "/CN=devuser/O=developers"

Generate devuser certficate file using CSR 
There are two ways do it 

**1) Manually using client-ca-file file client-key-file**

openssl x509 -req -in devuser.csr -CA /var/lib/minikube/certs/ca.crt -CAkey /var/lib/minikube/certs/ca.key -CAcreateserial -out devuser.crt -days 365

copy conetnet of devuser.crt and devuser.key to local to point add user in kubeconfig file

Command to add user to kubeconfig 

kubectl config set-credentials devsuer --client-certificate=C:/Work/K8Learning/devuser/devuser.crt --client-key=C:/Work/K8Learning/devuser/devuser.key 

Commabd to map devsuer to minikube cluster

kubectl config set-context devuser-minikube --user=devsuer --cluster=minikube

Now use newly created context using kubectl config use-context devuser-minikube and try listing pods  kubectl get pods --- we see error forbidden

Create role and binding role to devuser and we should be able to list pods.


<img width="1440" alt="Screen Shot 2024-05-11 at 8 21 33 AM" src="https://github.com/VamsiPothireddy/K8-HandsOn/assets/47288461/70505ba7-5ac6-4e1e-acfe-997beeb81925">

   
**2) Creating CSR object and signing**


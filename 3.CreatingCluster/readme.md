**Distribution of K8**

Like the way Linux has Distributions like centOS , Debinan ,Ubuntu etc , K8s is opensource and provoders like Amazon , Azure ,Redhat enhaned this and giving thier licenced versions of distrubutions as managed K8s

Amazon/AWS - EKS                                                
RedHat - Openshift              
Azure - AKS 

If we have to create cluster and use direct K8s distribution (not managed ones like EKS/AKS etc ), then we have to identify  master and workder ndes and install by ourself and manage those nodes (either baremetal / sw upgrades in Ec2 etc) . But there are tool like kops exist to do intsllation specifying count like (worker ,master nodes)
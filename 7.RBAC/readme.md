**User Management**
Authentication and Authorization is key for any system. In K8s user and group creation is not handled by K8s. Insted it offloads to Identity Providers ex IAM roles in EKS or KeyClock etc . 

These IDP creates users andd authenticates them , but authorization is handled through K8S using role and rolebinding.  We create a role with permissions like reading pod and assign (role binding) that to developers user group in IAM . Create another role with permissions delete pod and assign it to Admin group 

This is called **R**ole **B**ased **A**ccess **C**ontrol
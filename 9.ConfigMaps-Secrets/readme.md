 Config map and Secrets are storage objects at K8s .They store data in key value pair format                                       
 exmple below

```yaml
 apiVersion: v1
kind: ConfigMap
metadata:
  name: db-configmap
data:
  host: "brownpanthertech.host"
  port: "3306"
```
here host and port are keys and we have respective values "brownpanthertech.host" and "3307"                                                        
Note : Always specifcy values in double quotes

Once we create config map and these values can be retrieved in pod using two ways env variables and volume mounts

Now lets log in to pod and see if these env variables are available 

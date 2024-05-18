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
<img width="602" alt="Screen Shot 2024-05-18 at 7 33 04 AM" src="https://github.com/VamsiPothireddy/K8-HandsOn/assets/47288461/765bcd00-47c2-4e51-964d-08e96460f82b">


Now lets log in to pod and see if these env variables are available
<img width="919" alt="Screen Shot 2024-05-18 at 7 38 41 AM" src="https://github.com/VamsiPothireddy/K8-HandsOn/assets/47288461/a82c1eca-cd15-4a69-a43d-ec9d32504b5d">


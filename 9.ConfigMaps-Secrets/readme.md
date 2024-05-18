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


There is a problem with this approach , if we make any changes to config map , lets say updated port number to 3307 , env variables wont be changed in running container . So we can use volume mounts .Please refer **nodeapp-volumemount-deployment.yml** file 



```yaml
spec:
      containers:
      - name: node-service-logger1
        image: vamsipothireddy/node-service-logger1:latest
        ports:
        - containerPort: 3000
        
        volumeMounts:
        - name: config-volume
          mountPath: /etc/config
          readOnly: true
        resources:
          requests:
            memory: "128Mi"
            cpu: "250m"
          limits:
            memory: "256Mi"
            cpu: "500m"
      volumes:
      - name: config-volume
        configMap:
          name: db-configmap
```
We create a volume , in this case config-volume copied from existing db-configmap of type **configMap** . Now we mount volume to container path using volumeMounts. Now if we go and check containers  /etc/config path , we see two files created with names of keys in configmap ie host and port and that file contains respective value . Now if we make changes to any config map auotmatically file content will be refreshed.

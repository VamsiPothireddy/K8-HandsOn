
In Docker if we have to run conatiner we pass docker run command like below specidfying port number , image etc 

example                                                       
docker run -d --name node-service-logger1 -p 3001:3000 

In pod.yml file we can specifiy all thise things 

So pod is nothing but container creation in docker where all argumnets passed in run will be specified in pod.yml

But in realwold scenarion , we dont use pod.yml as its not giving any auto healing capability which is reason we moved to K8 from just using docker 

In depployment.yml file we cans specifiy how maany replica counts - ie how many pods has to be run , so even if we delete pod manually - another pod will be created but how ?  Its usining controller called replica set . 

When we create depployment.yml it inturn creates controller called replicaset whcih ensures it runs desired pods (number specified in deployment file) . It always checks descired vs current and make sure it reches disered pod count . 

In K8s replicaSet is one of the controllers . In general what contrillers does is checkng desired vs actual and meets actual

<img width="705" alt="Screen Shot 2024-05-12 at 9 23 48 AM" src="https://github.com/VamsiPothireddy/K8-HandsOn/assets/47288461/63aa722e-565c-400d-a008-ea8bb0d62e2e">




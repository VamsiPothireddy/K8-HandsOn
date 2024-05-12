In Docker, when we need to run a container, we use the docker run command, specifying port numbers, image, etc.

For example:

docker run -d --name node-service-logger1 -p 3001:3000
In a pod.yml file, we can specify all these details. A Pod is analogous to container creation in Docker, where all the arguments passed in docker run are specified in the pod.yml.

However, in real-world scenarios, we don't usually use pod.yml because it doesn't provide any auto-healing capability, which is why we moved from just using Docker to Kubernetes.

In a deployment.yml file, we can specify the desired replica counts – i.e., how many pods should be run. So even if we manually delete a pod, another pod will be created automatically. How? It uses a controller called ReplicaSet.

When we create a deployment.yml, it, in turn, creates a controller called ReplicaSet, which ensures that the desired number of pods (specified in the deployment file) are running. It continually checks the desired versus the current state and ensures that it reaches the desired pod count.

In Kubernetes, ReplicaSet is one of the controllers. Generally, controllers compare the desired state with the actual state and ensure that the actual state matches the desired state."

<img width="705" alt="Screen Shot 2024-05-12 at 9 23 48 AM" src="https://github.com/VamsiPothireddy/K8-HandsOn/assets/47288461/63aa722e-565c-400d-a008-ea8bb0d62e2e">




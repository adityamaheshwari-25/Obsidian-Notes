- that node machine/minions can be physical and virtual
- Api server acts as a frontend for the K8s service.
- So as the market starts growing we are having other tools apart from docker, and different runtime, so to support all those container runtime as well you are having Container Runtime Interface in k8s that supports all the runtime.
- ContainerD can be used as the runtime as its own separate from Docker, now containerd is a separate project only.
- Now K8s no longer requires Docker as its runtime.
- Pods have one to one relationship with the containers running your application.
- You scale up/down with the pods, you don't have containers in the existing pods to scale you application.
- But a single pod can have multiple containers but they are not usually multiple containers of the same kind.
- Still multi-container pods are a rare usecase.
- Controllers are the brain behind kubernetes.
- ReplicationController - load balacing, Scaling, adding replicas.
- ReplicationController is the older technology replaced by ReplicaSet.
- ReplicaSet is the new recommended way to setup replication.
- apiVersion in the k8s files is specific to whatever we are creating, like if its a Pod, then it is V1.
- apiVersion is the version of the K8s that supports certain kind. like for Pod V1 is supported, and for ReplicaSets version apps/V1 is supported.
- ReplicaSet controller can also manage pods that are not part of/created by the ReplicaSets, this is where the selector thing comes into picture.
- <img width="1298" height="729" alt="image" src="https://github.com/user-attachments/assets/9557c528-dbc2-4f1a-a793-889902947cbc" />
  labels and selectors
- Two extensions: YAML for k8s, Paste and Indent
- what's the internal detail of how replicaSet deletes the pod or scales down, like how he selects pod to be deleted, you can make a video on that.
- <img width="1197" height="722" alt="image" src="https://github.com/user-attachments/assets/15dc99b2-ea2e-45df-a63b-0a1bc176c636" />
- Deployment automatically creates the replicaset.
- We you create a deployment it creates a rollout.
- RollingUpdate is the default deployment strategy.
- <img width="1296" height="671" alt="image" src="https://github.com/user-attachments/assets/8d2f261a-ccd4-4075-b779-bc0c45c99948" />
- <img width="1354" height="723" alt="image" src="https://github.com/user-attachments/assets/b31e97c3-0682-4875-8060-ff0ccc60aef3" />
- Rollout is the process of deploying the containers in the backend.
- Actually you don't have to setup k8s networking and all, there are already solutions with related to that like Cisco CI and all, many are there.
- Kubernetes Services: helps communicate within and outside the application.
- Kubernetes Services is just like any other thing that we have studied earlier, like pods, deployments etc....helps to communicate that's it
- <img width="1296" height="671" alt="image" src="https://github.com/user-attachments/assets/10c2fcd1-d31b-4b56-9aaa-5002b6174eba" />
- Again in the Services as well, we use labels and selectors only to connect the service to the pods.
- <img width="1354" height="723" alt="image" src="https://github.com/user-attachments/assets/ec7a10c0-a6cb-4bb8-8e03-d2a519d4d25f" />
- And basically you can group pods based on services and so you can easily deploy the microservices based application.
- LoadBalancer type only works for the Cloud Platforms.
- Service is basically used for basically exposing the application.....depending on the requirement, you don't do it via the pod IP because it can change and also you won't be able to scale the application.
- ClusterIP is used when you don't want to make it accessible outside the cluster.
- <img width="1838" height="1017" alt="image" src="https://github.com/user-attachments/assets/140fa7c0-b590-49f5-86eb-034329d403ec" />
- https://github.com/kodekloudhub/example-voting-app/tree/master/k8s-specifications
- You add it as LoadBalancer when you want to expose it to the outside world.
- [ External Client ]
         │
         ▼ (Requests: http://<Node-IP>:<nodePort>)
┌─────────────────────────────────────────────────────────────┐
│ WORKER NODE (e.g., IP: 192.168.1.50)                        │
│                                                             │
│   [ nodePort: 30080 ] ◄── External Entry Point              │
│            │                                                │
│            ▼                                                │
│   ┌─────────────────────────────────────────────────────┐   │
│   │ KUBERNETES SERVICE (Virtual IP inside cluster)      │   │
│   │                                                     │   │
│   │   [ port: 80 ] ◄── Internal Cluster Entry Point    │   │
│   └────────┬────────────────────────────────────────────┘   │
│            │                                                │
│            ▼ (Routable to any matching Pod)                 │
│   ┌─────────────────────────────────────────────────────┐   │
│   │ POD                                                 │   │
│   │                                                     │   │
│   │   [ targetPort: 8080 ] ◄── App Container Port       │   │
│   │        │                                            │   │
│   │        ▼                                            │   │
│   │   ┌─────────────────────────┐                       │   │
│   │   │ Application (e.g., Nginx)                       │   │
│   │   └─────────────────────────┘                       │   │
│   └─────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────┘


-   In the managed K8s services, master node does not host any application, and you can't access the master node as well, it is managed by the service provider.
- And the worker nodes are just the EC2 instances only where we have just installed the kubectl and its managed by the master node.

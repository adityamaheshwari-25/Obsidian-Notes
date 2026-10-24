- We need docker or its equivalent(like containerd or rkt) to install in the nodes to run the containers.
- ![[Pasted image 20260924143742.png]]
- kube-proxy is for managing the communication between the services in the cluster.
- Docker was introduced even before the CRI standards.
- etcd stores the information of the server in the key-value pair store.
- There are certificates which are basically used for authenticating request in the cluster and accessing the components.
- Okayy so basically we can install separate components in the k8s cluster from the k8s website as well.
- Practise all your stuff on the minikube manhh, understand each and everything well and indepth, don't go with the kubeadm and all otherwise you gonna have the setup issue.
- Scheduler only decides which pod goes on which node, doesn't actually place the pods on the node.
- Actually you can make those indepth videos on k8s how it intelligently manages all the things.
- Actually that's how you can write your own Scheduler as well, based on your needs.
- For every component in the K8s you have one binary of it that you can download and run.
- worker nodes host applications as containers.
- Most of the components you run it as a service!
- We have one Virtual Pod network which spans across all the pods in the cluster.
- ![[Pasted image 20260924162948.png|363]]
- what is kubernetes namespace and how we can create it, please give me some practical thing to see how is it all there.
- As you are going through the course, keep practising locally on your minikube cluster.
- Multi-container pods.
- ![[Pasted image 20260925110545.png]]
- ![[Pasted image 20260925111218.png]]
- Checkout all the namespaces in the minikube.
- ![[Pasted image 20260925115430.png|497]]
- Basically for all the changes, always first update the file and then do the apply command, that's it, always this is the declarative way, apply command handles the rest, history of changes and everything it handles the rest.
- Nodes don't have the namespace, they are cluster scoped, and that's pretty obvious.
- ![[Pasted image 20260925164417.png]]
- ![[Pasted image 20260925164637.png]]
  This only happens when you do the apply configuration command.
- Do one thing, understand each and every topic from the Chatgpt and then watch all those lectures, you gonna understand it much much better, focus all on understanding things pretty pretty well, that's what is all matters! For each section in the course, first understand it from the Chatgpt all the topics, and understand it with related to the minikube as well.
- So there's one more thing, that we have to approprialtely set the node configurations as well so that it can support pods.
- Okayy, you have one schedular in the kube-system that automatically assigns the pod to the node basically does the scheduling thing, if there's no schedular the pod will be in the pending state or you have to manually schedule the pod actually.
- control plane has a taint at the starting only so it doesn't allow anyone to schedule a pod on it, but you can remove that taint from it and schedule the work on the control plane as well but its not a good practise.
- Node Selectors are simpler, for more complex things, use Node affinity.
- For advanced options and expressions, go for Node affinity.
- ![[Pasted image 20260928163018.png]]
  So basically when pods are created, they are created and placed at the right node, based on the node affinity or basically the configuration.
- ![[Pasted image 20260928163706.png]]
	In this basically "required" is, when you definitely want that and if it is not there then they the pods will not be scheduled, but in "preferred" if it is not there also they it won't be a problem it will schedule it to some other node, and DuringExecution is when the you change something when the pods are running but its set as Ignored, so even if you change anything the pods won't be affected.

 - Node affinity and Taints & Tolerations are used hand in hand.
 - CPU Throttles when the container uses more than the specified limit, but that is not in the case of memory, in case of memory, it just gives OOM(Out of Memory) and terminates.
 - ![[Pasted image 20260928174316.png]]
   This is applicable at the namespaces level, and this limit and cpu is wrote for the container inside the Pod, always remember this!
 - ![[Pasted image 20260928174506.png]]
 - LimitRange does not affect active pods, it only affects the newer pods that are made after the LimitRange has been created. This LimitRange is at the namespace level.
 - ResourceQuota helps you manage the overall cluster resources, like in total only this much cpu and memory should be used. It is also at the namespace level.
 - In this Kodekloud lab, they are being given one controlplane node and one worker node to practise all of the stuff.
 - Kube-apiserver is aware of the static pod creation by the kubelet, as when the static pod creates, it also creates a mirror object in the kube-apiserver.
 - You can only delete pod by removing the manifest file from the manifest folder.
 - Actually the use case of static pods is you can create as many master nodes as you want. And this is how the kubeadm setups the k8s cluster.
 - Priority classes are non-namespaces objects meaning they are not created within a namespace.
 - ![[Pasted image 20260929124057.png]]
   - By default if we don't assign a priorityClass it has a priority value of 0. You set that using the globalDefault property actually. And this globalDefault and preemptionPolicy is defined once only, ie. only in one PriorityClass.
   - K8s is highly extensible.
   - this kubeconfig has the authentication information to connect to the K8s API Server.
   - so basically you deploy your own custom scheduler as a pod only in the kubeadm....
   - we are running kube-scheduler either as a pod or as a deployment...
   - Actually you can create your own scheduler specifying your custom rules and configurations different from the default scheduler that k8s gives you. And you can use the same image as the default scheduler as well to create that custom scheduler, at last that container is running pod only...
   - When the pods are created first they go into the scheduling queue.
   - There are certain plugins that helps with the different stages that occurs in the scheduling of the pod.
   - A single plugin can be used in the multiple phases.
   - Actually we can make our own plugins as well, and plugin in there, that's what it is called as Extension point.
   - There are default plugins as well.
   - ![[Pasted image 20260929164519.png]]
   - With the k8s 1.18 release, they introduced Scheduler profiles, so within one scheduler now you have multiple profiles. Now all those profiles run in the same binary now, instead of creating multiple binaries for different schedulers.
   - ![[Pasted image 20260929164915.png]]
   - ![[Pasted image 20260929165020.png]]
   -  All the cluster related info is saved in the etcd store.
   - You can create RBAC in the cluster.
   - there are many things that you can't control, so there comes the Admission Controllers.
     ![[Pasted image 20260929173022.png]]
   - So there can many types of admission controllers and there are some default as well.
     ![[Pasted image 20260929173238.png]]
   - Some admission controllers are enabled by default, and some are not.
   - It not only accepts/rejects the request, it also make changes/mutates the request, or can perform operations in the backend or change the request itself.
   - Hey manhh, watch the solution videos as well you will understand better, don't miss them!!!!
   - NamespaceExists plugin is Validating kind of plugin.
   - Mutating admission controllers are that they can change the request.
   - First the validation admission controllers work and then the admission ones and that's quite logical.
   - Actually you can have external admission controllers, to support that you have two hooks available.
   - kubectl apply
      ↓
API server authentication
      ↓
Authorization
      ↓
Admission controllers
      ↓
Admission webhooks
      ↓
Object stored in etcd
      ↓
Scheduler runs the Pod

- A webhook is therefore an **external policy service**, while an admission controller is the **API-server mechanism that invokes it**.
- So this is how Admission controllers work internally, basically they call the webhooks for that.
- The important distinction is:

- **Admission webhook**: the integration/mechanism used by Kubernetes
- **Admission webhook server**: the actual application that receives the request and makes the decision
- **API server**: the Kubernetes component that calls the webhook server and enforces its response

In your case, the **image-policy backend** is acting as the admission webhook server.

- MONITORING, you have one thing called as Metrics servier.
- In Kubelet, you have one thing called cAdvisor or container adviser that takes the performance metrics of the pod and send it to Metric Server and expose it via API Server.
- Cluster performance can be viewed using kubectl top node command.
Gonna work so fking hard and get into good company, just pray hard and work hard that's it.




- APPLICATION LIFECYCLE MANAGEMENT
- A new rollout creates a new ReplicaSet.
- Container only lives when the process inside it keeps running, otherwise it just stops or crashes.
- So basically for the default value in the entry point you mention the CMD.
- If you mention if will override the CMD instruction.
- ![[Pasted image 20261001172645.png|535]]
- ![[Pasted image 20261001172902.png|540]]
- CMD has the Overriding behaviour, and ENTRYPOINT has the appending behaviour.
- ConfigMaps is used to store the configuration in the plane text so password kinda thing is not suitable there, that's where Secretes come into picture. In secrets they are stored in the encoded/hashed format.
- But still those secrets are just encoded, they can be decoded so they are not secure.
- So there are many solutions to it, like Secret Store CSI driver and all.
![[Pasted image 20261005105830.png|584]]
and as the name says its a driver, it basically pulls secrets from the AWS Secrets Manager or whatever you are using and mounts them as the volumes in your pod. And that volume contains the secret that we want that is pulled from the AWS Secrets manager.

- You have ECO and sealed secrets as well.
- We had some authentication in the cluster to connect with the etcd cluster.
- And also basically you have some encryption algorithm for the secrets actually, and we have many providers for encryption as well.
- Like you have volume mounts for the containers, same goes with the pod as well...
- If you are using containerd, then we can also use crictl.
- Enabling Encryption at Rest for Secrets is basically storing the encrypted form of secrets in the ETCD.
- Multi-container pods![[Pasted image 20261005122657.png|542]]
- They have the same network, volume and lifecycle, so when they both created and destroyed together.
- Multi-container pod design pattern:
  ![[Pasted image 20261005123115.png]]
- ![[Pasted image 20261005123505.png]]
  There's no particular order in which they start.
- ![[Pasted image 20261005123610.png]]
  In this once that init container does its job and stops, after that the main container starts.
- ![[Pasted image 20261005123719.png]]
  You can have multiple init containers as well.
- ![[Pasted image 20261005124013.png]]
  So this log init container just stops after when the main container stops just to log the termination of the main container and that init container starts before the main container and logs the startup and keeps running. You have that ELK monitoring stack based on this.
  ![[Pasted image 20261005124443.png]]
  Sidecar **Filebeat** already comes with the ElasticSearch(used for getting the logs from different endpoints) installed, Kibana is used for visualizing the logs.
- # Kubernetes Init and Sidecar Containers

- A Pod can run related containers that share networking and, when configured, storage.
- Containers in `containers` start together.
- The Pod's `restartPolicy` controls restarts:
  - `Always`: restart after any exit.
  - `OnFailure`: restart after a non-zero exit.
  - `Never`: don't restart.
- Kubernetes normally restarts the failed container in the same Pod, not every container in the Pod.

## Regular init containers

- Defined under `initContainers`.
- Run one at a time, in list order, before app containers start.
- Each must finish successfully before the next init container runs.
- Used for setup tasks, such as waiting for a dependency or preparing files.
- If one fails, Kubernetes retries it according to the Pod's restart policy; app containers wait.

## Native sidecars

- Also defined under `initContainers`.
- Set `restartPolicy: Always` on the init container to make it a sidecar.
- Starts before the app, then keeps running alongside it.
- Restarts independently if it exits.
- Kubernetes shuts down the app containers before the sidecar.
- Useful for logging agents, proxies, and other supporting processes.
- Native sidecars have been stable since Kubernetes v1.33.

## Example to remember

- Regular init container: "Prepare first, finish, then let the app start."
- Sidecar: "Start first, then keep helping the app while it runs."

---------

- Sidecar containers use uses `restartPolicy: Always` to stay alive throughout the Pod lifecycle.
- Kubernetes starts the sidecar first, waits for readiness, then starts the main app.
- And those init containers run sequentially.
- There are two approaches to scaling in k8s, one is workload scaling, other is scaling the underlying cluster itself which is basically adding more server infrastructure to your cluster.
  ![[Pasted image 20261005150212.png]]
- For vertical scaling, first you take down the server and then upgrade the infra and then start the server again.
- ![[Pasted image 20261005150428.png]]
- ![[Pasted image 20261005151038.png|456]]
- So this Horizontal Pod Autoscaler polls the Metrics Sever for the resource consumption and depending on that do the thing as mentioned.
- Imperative way of creating HPA.![[Pasted image 20261005151805.png]]
- Declarative way![[Pasted image 20261005152009.png]]
- So we have internal adapter and external adapter based on what metrics server can decide to autoscale.![[Pasted image 20261005152305.png]]
- There's one monitoring tool called Skooner, used for monitoring K8s cluster.
-  VPA is not built in K8s like HPA, so there's no imperative command for VPA.
- ![[Pasted image 20261005163056.png]]
- ![[Pasted image 20261005163328.png]]
- Like when doing AI/ML stuff you may need high CPU then later you don't need high CPU/Memory that's where you can use VPA.

--------
### Cluster maintainence
- If the node goes down, then the master node waits upto 5 minutes before considering the node dead, and this time is called tolerationSeconds.
- ![[Pasted image 20261005225634.png]]
- ![[Pasted image 20261005225651.png]]
- drain moves the pods to another nodes.
- cordon just does not schedule pod, it doesn't move the pods to another node.
- **Cordon** stops Kubernetes from scheduling **new Pods** onto the node, while leaving currently running Pods completely untouched.
- **Drain** safely **evicts all existing Pods** from the node and moves them to other nodes, automatically blocking new ones from arriving.
- **Uncordon** makes a previously restricted node **fully available again** to accept and host new Pods.
- the kubectl drain command automatically cordons the node first before evicting any running pods.
- And basically uncordon command is basically used to reverse the effect of drain and/or cordon.
- When you install k8s cluster, you install some specific version of the k8s.
- ![[Pasted image 20261006000528.png|200]]
- Basically for any package of the k8s, you will find these components. ![[Pasted image 20261006000821.png]]
- As we can see even different components have their versions, etcd and CoreDNS are the external components. 
- Cluster Upgrade: basically upgrading the k8s version
- none of the components should have the higher version than the Kube-apiserver, but that is not the case with the kubectl.
- We can also upgrade component by component in the cluster.
- Upgrading the server involves two steps, one, upgrading the master node, second, upgrading the worker nodes.
- We can only upgrade one minor version at a time.
- UNDERSTAND THINGS!!
- Basically you can upgrade the k8s cluster without making your application down.
- First you always upgrade the control plane, and after that you upgrade the worker nodes.
- when you do `kubectl get node`, its the version of the kubelet that it is running, that version section that you see.
- Understand the whole process of upgrading the cluster.
	- Upgrading one node at a time, while moving the workload to other nodes.
	- running kubeadm upgrade plan, getting the latest k8s version that it can upgrade, and you have to upgrade the kubeadm tool as well for compatibility to upgrade the cluster as well.
	-  kubectl drain controlplane --ignore-daemonsets, first we are gonna upgrade the controlplane node.
	- Upgrade the kubeadm tool (if not already), then the controlplane components, and finally the kubelet. Practice referring to the Kubernetes documentation page.
	- you upgrade kubeadm and kubelet for each node in the cluster.
	- upgrading the control plane means upgrading the k8s version only.
- So final points:
	- # Kubernetes Cluster Upgrade Using kubeadm

## 1. Understand the three tools

- **kubeadm:** Sets up and upgrades Kubernetes cluster components.
- **kubelet:** Runs on every node and manages the pods on that node.
- **kubectl:** A command-line client used to communicate with the Kubernetes API server.

**Kubernetes consists of several components. There is no single package called “Kubernetes” that you update once to upgrade every node.**

## 2. Which command upgrades what?

> The installation examples below are for Ubuntu/Debian.
> Replace `x` with your chosen patch version. Configure the package repository for the target minor version and unhold packages before updating them; hold them again afterward.

### Upgrade the kubeadm tool

```bash
sudo apt-get install -y kubeadm='1.35.x-*'
```

- Updates the kubeadm program installed on that machine.
- Run this on each node before performing that node’s upgrade.
- Installing a newer kubeadm does not automatically upgrade the cluster.

### Check the available Kubernetes upgrades

```bash
sudo kubeadm upgrade plan
```

- Shows the current cluster version and possible upgrade targets.
- The remote version refers to an available Kubernetes release.
- This command checks and displays information; it does not perform an upgrade.

### Upgrade the first control-plane node

```bash
sudo kubeadm upgrade apply v1.35.x
```

- Run this once on the first control-plane node.
- Upgrades that node’s control-plane components, including the API server, scheduler, and controller manager.
- Updates shared cluster configuration.
- Manages shared add-on upgrades, such as CoreDNS and kube-proxy. In current versions, these wait until all control-plane instances have been upgraded.
- Does not install newer kubelet binaries on your nodes.

### Upgrade additional control-plane nodes and worker nodes

```bash
sudo kubeadm upgrade node
```

- Run this locally on each remaining node.
- On an additional control-plane node, updates its control-plane components and kubelet configuration.
- On a worker node, updates its kubelet configuration.
- Does not install the newer kubelet binary.

### Upgrade the kubelet

```bash
sudo apt-get install -y kubelet='1.35.x-*'

sudo systemctl daemon-reload
sudo systemctl restart kubelet
```

- Updates the kubelet installed on that machine and restarts it.
- Perform this on every control-plane node and every worker node.
- Drain the node before upgrading its kubelet across minor versions.

### Upgrade kubectl

```bash
sudo apt-get install -y kubectl='1.35.x-*'
```

- Updates the kubectl client on that machine.
- Update it wherever it is installed and used.
- Updating kubectl does not upgrade the cluster.

## 3. Upgrade order

### First: Prepare the cluster

- Choose the target Kubernetes version.
- Check cluster health and compatibility.
- Back up etcd and important application data.
- Ensure the remaining nodes can handle workloads while one node is drained.
- Upgrade one minor version at a time.

Example: `1.34 → 1.35 → 1.36`, without skipping a minor version.

### Second: Upgrade the first control-plane node

1. Update its kubeadm package.
2. Run `kubeadm upgrade plan`.
3. Run `kubeadm upgrade apply v1.35.x`.
4. Drain the node before upgrading its kubelet.
5. Update kubelet and kubectl, if installed.
6. Restart kubelet.
7. Verify the node is healthy and uncordon it.

### Third: Upgrade additional control-plane nodes

Perform these steps on one control-plane node at a time:

1. Update its kubeadm package.
2. Run `kubeadm upgrade node`.
3. Drain the node before upgrading its kubelet.
4. Update kubelet and kubectl, if installed.
5. Restart kubelet.
6. Verify the node is healthy and uncordon it.

### Fourth: Upgrade worker nodes

Perform these steps on one worker at a time:

1. Update its kubeadm package.
2. Run `kubeadm upgrade node`.
3. Drain the worker.
4. Update kubelet and kubectl, if installed.
5. Restart kubelet.
6. Verify the worker is healthy and uncordon it.
7. Continue with the next worker.

### Finally: Verify everything

```bash
kubectl get nodes
kubectl get pods -A
```

- All nodes should return to `Ready`.
- The node versions shown by `kubectl get nodes` are their kubelet versions.
- Check that application pods and cluster components are healthy.

## 4. How applications continue serving traffic

Before updating a node’s kubelet, drain that node:

```bash
kubectl drain <node-name> --ignore-daemonsets
```

- Prevents new ordinary pods from being scheduled onto that node.
- Evicts eligible pods, respecting PodDisruptionBudgets.
- Controllers such as Deployments create replacement pods on other available nodes.

After the upgrade, allow scheduling again:

```bash
kubectl uncordon <node-name>
```

Applications can continue serving traffic when:

- Enough healthy replicas remain available.
- Other nodes have enough capacity for replacement pods.
- Readiness checks and disruption settings support the maintenance.
- Storage and application state allow pods to run elsewhere.

A single application replica can experience downtime during draining. With a single control-plane node, the Kubernetes API can be briefly unavailable during its upgrade even while existing application pods keep running.

## 5. Once or on every node?

| Action | Where to perform it |
|---|---|
| Update kubeadm package | Every node being upgraded |
| `kubeadm upgrade plan` | Usually the first control-plane node |
| `kubeadm upgrade apply` | Once on the first control-plane node |
| `kubeadm upgrade node` | Every additional control-plane node and worker |
| Update and restart kubelet | Every node |
| Update kubectl | Wherever it is installed and used |

## Quick reminder

- **Install kubeadm:** Updates the local upgrade tool.
- **kubeadm upgrade apply:** Starts the cluster upgrade and updates the first control-plane node.
- **kubeadm upgrade node:** Updates another node’s Kubernetes components/configuration as appropriate.
- **Install kubelet:** Updates that node’s pod-management service.
- **Install kubectl:** Updates the local command-line client.
- **Order:** First control-plane node → remaining control-plane nodes → worker nodes.


### Backups & Restore Methods

![[Pasted image 20261006125408.png|354]]
you have tools such as ARK that helps taking the cluster backups using the k8s API.
- you can backup etcd as well, as it contains the information for that cluster.
- etcd is hosted on the master nodes.
- you have snapshot file there as well.
- ![[Pasted image 20261006125830.png]]
- your kube-apiserver depends on the etcd.
- ![[Pasted image 20261006130059.png]]
- ![[Pasted image 20261006130125.png]]
- So there are two methods, backup using etcd, and another one is querying kube-apiserver.
- In the managed k8s cluster, you don't have the access to etcd, so the only way in that is querying the kube-apiserver only.
- And there's backup and then restore as well.
- `etcdctl` is a command line client for [etcd](https://github.com/coreos/etcd).
- So basically for all the components in the k8s you have one version.
- 
# ETCD Backup and Restore — Quick Notes

## 1. Tools

- **etcdctl:** Communicates with a running etcd server; used to create backups.
- **etcdutl:** Works directly with local data files; used to inspect and restore snapshots.
- In these Kubernetes labs, etcd runs as a static pod on the control-plane node.

### Check the client version

```bash
etcdctl version
```

- Shows the installed etcdctl version and its API version.
- `ETCDCTL_API=3` selects API v3 in versions that support this setting.

## 2. Take a Backup

- Use `etcdctl snapshot save` to create a snapshot from a running etcd server.
- Ensure `/backup` exists and use the correct endpoint and certificate paths.

```bash
ETCDCTL_API=3 etcdctl \
  --endpoints=https://127.0.0.1:2379 \
  --cacert=/etc/kubernetes/pki/etcd/ca.crt \
  --cert=/etc/kubernetes/pki/etcd/healthcheck-client.crt \
  --key=/etc/kubernetes/pki/etcd/healthcheck-client.key \
  snapshot save /backup/etcd-snapshot.db
```

### Options

- `--endpoints`: Address of the etcd server.
- `--cacert`: CA certificate used to verify the server.
- `--cert`: Certificate used to authenticate the client.
- `--key`: Private key for the client certificate.

## 3. Inspect the Snapshot

```bash
etcdutl snapshot status /backup/etcd-snapshot.db \
  --write-out=table
```

- Displays the hash, revision, number of keys, and database size.
- Use `etcdutl` rather than the deprecated `etcdctl snapshot status`.
- Snapshot integrity is checked during restore for snapshots created with `etcdctl snapshot save`.

## 4. Restore the Snapshot

```bash
etcdutl snapshot restore /backup/etcd-snapshot.db \
  --data-dir=/var/lib/etcd-restored
```

- Creates a new etcd data directory containing the restored data.
- Runs locally; does not require endpoint or TLS options.
- Creates files only—it does not automatically restart etcd or connect Kubernetes to the restored database.
- During cluster recovery, stop the API servers before restoring.
- Configure etcd to use the restored directory, then restart etcd and the API servers.
- For a static pod, update the data volume’s `hostPath.path` in `/etc/kubernetes/manifests/etcd.yaml`.

## 5. Corrections to Remember

- **`etcdutl backup` is not a standard command.**
- Prefer `etcdctl snapshot save` for backups.
- Copying only `member/snap/db` can miss newer changes stored in the WAL.
- Restore requires configuring etcd to use the restored data; simply copying files back is not a general recovery procedure.

## Quick Command Summary

| Task | Command |
|---|---|
| Create a live backup | `etcdctl snapshot save` |
| Inspect a snapshot | `etcdutl snapshot status` |
| Restore a snapshot | `etcdutl snapshot restore` |
- actually etcd database has the built-in snapshot functionality.
- So basically, you can restore the original state of the cluster using the backup file.


**Complete Restore Process**

**Step 1: Stop the kube-apiserver**

Execute the following commands:

```bash
mv /etc/kubernetes/manifests/kube-apiserver.yaml /tmp/
sleep 30
```

**Step 2: Restore the etcd snapshot**

Run the command below to restore the snapshot:

```bash
etcdutl snapshot restore /opt/snapshot-pre-boot.db --data-dir /var/lib/etcd-from-backup
```

**Expected output:**

```
2025-04-24T09:38:07Z    info    snapshot/v3_snapshot.go:265     restoring snapshot
2025-04-24T09:38:07Z    info    membership/store.go:141 Trimming membership information from the backend...
2025-04-24T09:38:07Z    info    membership/cluster.go:421       added member
2025-04-24T09:38:07Z    info    snapshot/v3_snapshot.go:293     restored snapshot
```

**Step 3: Update the etcd configuration**

Open the etcd configuration file for editing:

```bash
vi /etc/kubernetes/manifests/etcd.yaml
```

**Modify the volumes section as follows:**

**From:**

```yaml
  volumes:
  - hostPath:
      path: /etc/kubernetes/pki/etcd
      type: DirectoryOrCreate
    name: etcd-certs
  - hostPath:
      path: /var/lib/etcd                    # OLD directory
      type: DirectoryOrCreate
    name: etcd-data
```

**To:**

```yaml
  volumes:
  - hostPath:
      path: /etc/kubernetes/pki/etcd
      type: DirectoryOrCreate
    name: etcd-certs
  - hostPath:
      path: /var/lib/etcd-from-backup        # NEW restored directory
      type: DirectoryOrCreate
    name: etcd-data
```

Upon saving this file, the etcd pod will restart automatically due to static pod behavior.

**Step 4: Restart the kube-apiserver**

Move the kube-apiserver manifest back to its original location:

```bash
mv /tmp/kube-apiserver.yaml /etc/kubernetes/manifests/
```

Wait for 60 seconds to allow the kube-apiserver to start.

**Step 5: Restart other control plane components**

Execute the following commands to restart additional components:

```bash
# Restart kube-controller-manager
mv /etc/kubernetes/manifests/kube-controller-manager.yaml /tmp/
sleep 20
mv /tmp/kube-controller-manager.yaml /etc/kubernetes/manifests/

# Restart kube-scheduler
mv /etc/kubernetes/manifests/kube-scheduler.yaml /tmp/
sleep 20
mv /tmp/kube-scheduler.yaml /etc/kubernetes/manifests/

# Restart kubelet
systemctl restart kubelet
```

**Step 6: Monitor the restart process**

Use the following command to monitor the restart:

```bash
watch crictl ps
```

**Key indicators to observe:**

- All components should show `STATUS = Running`
- The entire process should take approximately 2-3 minutes.

**Step 7: Verify the restore**

Run the commands below to check resource status across all namespaces:

```bash
# Check all resources across all namespaces
kubectl get deployments,services --all-namespaces

# Verify specific resources if needed
kubectl get pods --all-namespaces
kubectl get nodes
```

You should now observe all the resources that existed at the time the snapshot was taken.


- you remember right, kube-apiserver is also a static pod, so just we have to move the manifest file to this location /etc/kubernetes/manifests/, where kubelet will see and create the kube-apiserver again.


While the API server is stopped:

- `kubectl` commands cannot communicate with it.
- Kubernetes cannot schedule new pods through the normal control-plane flow.
- Existing application containers generally continue running. [Kubernetes](https://kubernetes.io/docs/tasks/administer-cluster/configure-upgrade-etcd/?utm_source=chatgpt.com)

So, therefore there won't be any discrepancy for the etcd as it contains all the info of the cluster.

**For a cluster with multiple API servers, stop all of them during recovery.**


and why do we restart all the other control plane components?
**Because restoring etcd returns the stored cluster state to an earlier point, while other components may still remember the newer state.**

These components keep information in memory—called **caches**—and watch for changes through the API server. After a restore, their remembered information can disagree with the restored database. Restarting helps them reload state and reconnect.

For example:

- Your snapshot says a Deployment needs **2 replicas**.
- Before restoring, you changed it to **5 replicas**.
- After restoring, etcd says **2**, but a component’s cache may still remember **5**.

Restarting helps the components use the restored information consistently. Kubernetes recommends restarting the scheduler, controller manager, and kubelet after restoring etcd to avoid relying on stale data.

One clarification: **kubelet is a node component**. Running `systemctl restart kubelet` on the control-plane node restarts only that node’s kubelet; it does not restart kubelets on the workers.


In the exam, you won't know if what you did is correct or not, as in the practice tests in this course.
You must verify your work yourself. For example, if the question is to create a pod with a specific image, you must run the `kubectl describe pod` command to verify the pod is created with the correct name and correct image.

------
# Security
K8s related security.
- via kubectl you interact with the k8s api server, so we have to restrict that first actually, because through that you can almost perform any operations, so that's the first line of defense.
- ![[Pasted image 20261006144931.png]]
- Who can access? => authentication![[Pasted image 20261006145038.png]]

- what they can do?![[Pasted image 20261006145110.png]]

- 
![[Pasted image 20261006145248.png|478]]

- ![[Pasted image 20261006145347.png|307]]

So till now these were the high level primitives in the K8s security - **TLS, Authentication, Authorization, Network Policies**
k8s nodes can be physical and virtual.

K8s does not manage user accounts natively, but supports service accounts
![[Pasted image 20261006150113.png]]

![[Pasted image 20261006150519.png|358]]
so when you do the kubectl command if goes to the Kube-apiserver and it first authenticates.
Remember to set authorization for the new users.
![[Pasted image 20261006151049.png]]
- This is symmetric encryption.![[Pasted image 20261006151904.png]]
![[Pasted image 20261006151959.png|478]]

and this is where asymmetric encryption comes in, 
![[Pasted image 20261006152133.png]]

- Initially you basically use both the symmetric and asymmetric encryption to secure the communication between the server and the user.
- So basically what is happening is, we actually want the symmetric encryption only, so for that we have to transfer that symmetric somehow safely to the server, so for that safe transfer we are using asymmetric encryption, in that basically we generate public and private key on the server, then 
	- so now when the user reaches to the server, the server sends him(user) the public key
	- now the user's browser encrypts the symmetric key using the public key provided by the server. Now the symmetric key is secured. 
	- Now that encrypted symmetric key is sent to the server, so the server only can decrypt that symmetric key as it only has the private key to decrypt that, while the hacker who is trying to hack does not have the private key so he cannot do anything.
	- So now finally the symmetric key is available only to the server and user. So now they can use the symmetric key to encrypt data and send to each other, and the receiver can use the same symmetric key to retrieve that information.
	- So using the asymmetric encryption, we have successfully transferred the symmetric key from the user to the server, and with the symmetric encryption we have secured all the future communication between them.
	- Now the thing related to the TLS certificate is, hacker can create a same identical dummy website and get your credentials, so what if is there's a way to validate the key that it is coming from the proper official website only and not the hacker's website, so this is where we use TLS certificate, in the TLS certificate you have the public key.
	  ![[Pasted image 20261006160842.png]]
	  But still hacker can create the same TLS certificate right, now it comes whether the certificate is legit or not, that's where the thing comes who signed and issued this certificate, 
	  ![[Pasted image 20261006161147.png|588]]
	  if you are signing this certificate, then its a **self signing certificate**, here anyone can see and tell you have signed this cert so its not safe, so the certificate that was issued by the hacker was fake as that was issued and signed by the hacker itself.
	  So in that case, your browser validates that if the certificate is fake or real, so in that case, browser has the in-built,  All of the browsers are built in with a certificate validation mechanism, wherein the browser checks the certificate received from the server, if its fake then it will warn you
	- so to create legitimate certificate, you have Certificate Authority(CA), so these are well-known organizations that can sign and validate your certificates for you.
	  ![[Pasted image 20261006170422.png]]
	- So how this works is, you generate a Certificate Signing Request(CSR) using the key you generated earlier, certificates generated by CAs are trusted by the browsers.
	- If the hacker does the same, his certificate would be rejected in the validation phase only.
	- The CAs use different techniques to make sure that you're the actual owner of that domain.
	- But how do the browsers know that the CAs itself is legitimate? So CAs have their public and private keys, the public keys of all CAs are built into the browsers. These are the public CAs that check the public websites. However they can't check the websites hosted privately within your organization, for that you need your own private CAs(you have your private CA server deployed).
	- And we have admin as well that generates a key pair for the secure SSH to the server.
	- The CAs generate their own key pair to sign certificates.
	- The server generates their own key pair for secure HTTPS traffic.
	- The end user though only generates a single asymmetric key pair.
	- But how will the server will know that the user is legit not hacker? so in that case one trust building exercise happens, web server request for the certificate to the user, So client generates a pair of keys and a signed certificate from the valid CA. Then the client sends the certificate to the Web server for validation...and this happens all under the hood you don't have to worry about it.
	- Till now what all we have studied is known as PKI.
	- You can encrypt data with any key public or private, and decrypt data only with the other not the same.
	- ![[Pasted image 20261006175459.png|477]]
	- ![[Pasted image 20261006175840.png]]
- So there are three certificates, first that configured on the server ie. server certificates, on the client that are client certificates, and on the CA which are root certificates.
- ![[Pasted image 20261007111648.png]]
- All the external as well as internal connections must be secured by 
- In certificates you have the public key.
- ![[Pasted image 20261007112309.png|492]]
- In this case, Admin, kube-scheduler, kubecontroller-manager and kubeproxy are all clients of kube-apiserver, and kubeapi-server acts as a client to etcd server and kubelet server you know the reasons, and in fact only kube-apiserver only communicates with the etcd server. So all those clients need client certificates.![[Pasted image 20261007112750.png]]

- So client need client certificate to authenticate to server, and server needs server certificates to authenticate to client.![[Pasted image 20261007113228.png]]
- So for the k8s cluster, we need **atleast** one CA, we can have more than one as well.
- CA has its own pair of certificates.
- ![[Pasted image 20261007113505.png]]


### Creating TLS certificate in the K8s.
- Creating TLS certificate for the CA itself first.![[Pasted image 20261007122005.png]]
- As its for the CA, the CA signs by its own with its private key.
![[Pasted image 20261007122031.png|561]]
- Then will go for creating the client certificates first with the Admin User, now in the command you specify the CA certificate and the CA key.
- Now how will you differentiate between the normal user and the admin user, so there you have the **Group** in the certificate, you can add that in the CSR using the OU.
  ![[Pasted image 20261007122937.png|428]]
- ![[Pasted image 20261007123124.png]]
- So the simple process is Generate Keys -> CSR -> Sign Certificates.
- ![[Pasted image 20261007123252.png]]
- So now what do you do with the certificates? So basically accessing the kube-apiserver instead of sending username and password, you authenticate via certificate in a REST-API call you make to the Kube-apiserver.
  ![[Pasted image 20261007123624.png]]
- The other way is moving this configuration in a file called the KubeConfig.
  ![[Pasted image 20261007123911.png]]
- In k8s, in order to verify k8s components among themselves they all have to have the CA certificate.![[Pasted image 20261007124517.png]]
- Lets see the server certificate now, you have to create for the Kube-api server and the etcd server, every operation goes through the Kube-apiserver, 
![[Pasted image 20261007125343.png]]
  you have to name all actually, like the kubernetes, kubernetes.default, kubernetes.default.svc, kubernetes.default.svc.cluster.local and their IPs which are on their right.
  ![[Pasted image 20261007125600.png]]
  
  for mentioning all the names, 
  ![[Pasted image 20261007125647.png]]
  ![[Pasted image 20261007125923.png]]

- Kubelet Nodes (Server certificates)
  The name of their certificates will be name after their nodes not the kubelet, 
  ![[Pasted image 20261007130935.png]]
  you must do it for each node in the cluster.
- The naming inside the certificates is very important, as these are used in the cluster and based on the naming you put the conditions and you write the manifest files, 
  ![[Pasted image 20261007131423.png]]
1. **It identifies the node:** `system:node:node01` is the identity Kubernetes uses for the kubelet running on `node01`. The prefix `system:node:` marks it as a node identity.

2. **It appears in the certificate’s Common Name (CN):** When the kubelet connects to the Kubernetes API server, it presents its client certificate. The API server reads the CN to identify which node is making the request.

3. **The certificate proves the identity:** The kubelet must have the private key that matches the certificate. This helps the API server verify that the connection is from the real `node01` kubelet.

4. **Kubernetes uses it to control access:** After authentication, the Node authorizer limits what the kubelet can access—for example, information about Pods scheduled on `node01` and the resources those Pods need.

5. **The name should match the registered node:** If the certificate says `system:node:node01`, Kubernetes expects the node to be registered as `node01`. A mismatch can cause authentication or authorization problems.

- If you starting out with the setting up the cluster then you have to manage all the certificates by your own, otherwise if you want it in a simple way then you Kubeadm does it for you.
- Once you issued the certificates look at the logs, and all the services are as pods in the Kubeadm tool.
- If the kube-apiserver or the etcd server which are the core elements does are down, then the kubectl doesn't work, in that case you have to go one level down and fetch the logs using docker, using the `crictl logs <container-id>`
- And as there can be more than one CA for the cluster, so in that case one possibility is having one CA for the ETCD server and one for the rest of the components in the Kubernetes.
  
- What is the Common Name (CN) configured on the Kube API Server Certificate?
  `openssl x509 -in /etc/kubernetes/pki/apiserver.crt -text`
- `openssl x509 -in /etc/kubernetes/pki/apiserver.crt -text` displays the API server certificate’s details in a readable format.
- `openssl x509` tells OpenSSL to work with an X.509 certificate.
- `-in /etc/kubernetes/pki/apiserver.crt` specifies the certificate file to inspect.
- `-text` prints its contents, such as the subject (CN), issuer, validity dates, public key, key usage, and Subject Alternative Names (SANs).
It only **reads and displays** the certificate; it doesn’t modify it.

- - `cat /etc/kubernetes/pki/etcd/server.crt` displays the certificate in its raw PEM-encoded form.
- `openssl x509 -in /etc/kubernetes/pki/etcd/server.crt -text` parses it and displays its certificate details in a readable format.
- why does the kubeapi server stops if it has the wrong ca for the etcd server?
  Because **the API server must trust etcd’s identity before it can use etcd as its database.**
  1. **The API server verifies etcd’s certificate** using the CA configured in `--etcd-cafile`. If the CA is wrong, verification fails with an error such as `x509: certificate signed by unknown authority`.
2. **The TLS connection is rejected**, preventing the API server from reading or writing cluster state in etcd. During startup, this can cause the API server to fail initialization and exit.
3. **The kubelet restarts the API server container**, but the failure repeats until you configure the correct etcd CA—typically `/etc/kubernetes/pki/etcd/ca.crt` in a kubeadm cluster.


#### Certificate Authority
- We have the CA server in our cluster, CA server is nothing but the pair of ca certificate and key, whoever gets access to this server can sign any certificate for the cluster.
- So these files need to be secured, so we place these files in a server in the cluster so that is our CA server.
- In case of Kubeadm, it stores the CA files in the Master node, so that Master node becomes the CA server as well.
- So what we are doing currently is, manually signing the certificates, and as the certificates have some expiry time so we have rotate that as well, so till now we are doing all manually which is not convinient as we move forward and have bigger app and team, so there we have something called the Certificates API
  ![[Pasted image 20261007152140.png]]
- So the whole process is:
  1. you create a key
  2. Then generates a certificate signing request using the key with her/his name on it, and sends the request to the administrator
  3. The administrator takes the certificate signing request and creates a CertificateSigningRequest object, its like other K8s objects only that can be created as the manifest file.
     ![[Pasted image 20261007152719.png]]
  This request field is the base64 encoded field, it mentions the name for the requestee.
  4. Once the object is created, all the CSR can be seen by administrators by running `kubectl get csr`
  5. and then can approve it as seen...
     ![[Pasted image 20261007152949.png]]
  6. k8s sign the certificate using the CA key pair and generates a certificate for the user. This certificate can be extracted and shared with the user.
  7. Generated certificate, certificate is base64 encoded here,
	    ![[Pasted image 20261007153249.png]]
  8. ![[Pasted image 20261007153340.png]]
  9. All these specific tasks are carried out by Controller manager, basically and these two approving and signing are the controllers.![[Pasted image 20261007153432.png]]

10.  For signing we need ca.crt and ca key right, here we have it in controller manager.
    ![[Pasted image 20261007153856.png]]

- **Custom group names are your choice**, such as `developers` or `devops-team`. Names are case-sensitive. Avoid the reserved `system:` prefix, which Kubernetes uses for built-in groups.
    
- **For client certificates, set the user’s group in the CSR’s Organization (`O`) field**, for example `/CN=akshay/O=developers`. Permissions come from RBAC bindings matching that group name.
    
- **`spec.groups` in the CertificateSigningRequest YAML records the submitting user’s groups**, not Akshay’s certificate groups. The API server fills it automatically, so you can omit it.
- And having group name as admins doesn't give you admin access.



#### KubeConfig file:
A **kubeconfig file tells `kubectl` how to connect to a Kubernetes cluster and authenticate with its API server**. It saves connection details so you don’t have to supply them with every command

- **A kubeconfig file tells `kubectl` how to connect securely to a Kubernetes cluster**, including the API server address, trusted CA, and authentication credentials such as a client certificate and private key.

- **It stores clusters, users, and contexts.** Each context combines a cluster, user, and default namespace. `current-context` selects which combination `kubectl` uses by default.

- **It lets you switch between clusters and users easily** using `kubectl config use-context <context-name>`. Its default location is `~/.kube/config`; use `--kubeconfig=<file>` to select another file.

![[Pasted image 20261007164316.png]]
![[Pasted image 20261007164737.png]]
- In this you don't have to create any object, it is automatically read by the kubectl command.
- Even it has namespaces, so basically we can switch context as well as the namespaces.![[Pasted image 20261007165721.png]]
- `kubectl config view` is the most used command.
- context is what binds cluster and the user.
- So basically you can switch multiple clusters with it.
#### API Groups:
So as we have seen we can communicate the kube-apiserver via the REST call or via the kubectl command.
![[Pasted image 20261007172421.png]]
k8s API is grouped in many ways.
![[Pasted image 20261007172637.png]]
- ![[Pasted image 20261007172730.png]]
- ![[Pasted image 20261007173521.png]]
- ![[Pasted image 20261007173917.png]]
- Using these API Groups only we do the Authorization.
#### Authorization
As we don't have the same level of access to the cluster to everyone, so we have the authorization.
So there are different mechanisms supported by the kubernetes such as Node Authorizer, ABAC, RBAC and webhook, 
That kubelet in their certificate have the name prefixed with system:node which standard in k8s, 
- For inside the cluster we have the Node Authorizer.
- ABAC(Attribute Based Authorization), this is for the external access, and in this basically you can mention the list of the actions that can be done, this is difficult to manage as you have to make any modifications manually and restart the Kube-apiserver.
![[Pasted image 20261007225006.png]]
- RBAC: here this makes it much more easier,  
  ![[Pasted image 20261007225240.png]]
- Webhook: It is used when you want to outsource all the authorization things and don't want to use the built-in thing.
  ![[Pasted image 20261007225418.png]]
- You have two other modes, as the name suggests,
  ![[Pasted image 20261007225511.png]]
- You can have multiple modes configured.![[Pasted image 20261007225746.png]]
  ![[Pasted image 20261007230032.png]]


#### RBAC
We create a Role object for it.
And to attach a user to that Role, we create another object called the RoleBinding.
The RoleBinding object links a user object to a Role.
![[Pasted image 20261007231035.png]]
Role and RoleBinding fall under the namespaces.
In subjects section, you write the User details, and in the RoleRef you write the Role details.
![[Pasted image 20261007231544.png|410]]

![[Pasted image 20261007231734.png]]
We can go a level down as well and assign the role actually.

-  `kubectl get roles --all-namespaces --no-headers | wc -l
  use this command for counting
  `--no-headers` removes the column heading, so the count includes only the Roles.
  and wc is word count and -l is the line.

# Kubernetes API Groups Explained

In Kubernetes, an **`apiGroup`** is a way of grouping related HTTP paths and resources together in the Kubernetes API. Think of them like **folders or namespaces for different types of resources** to keep the API organized, scalable, and easy to extend.

When you interact with Kubernetes (e.g., using `kubectl`), every request goes to a specific URL path that looks like `/apis/<apiGroup>/<version>/...`.

---

## How they are used in your Role YAML

In your `developer` Role, you used two different API groups because the resources you want to manage belong to different parts of the Kubernetes system:

### 1. The Core API Group (`""`)
```yaml
- apiGroups: [""]
  resources: ["pods"]
```
* **What it means:** An empty string `""` represents the **Core (or Legacy) API group**. 
* **Why it's used:** The most fundamental, foundational resources in Kubernetes—like `pods`, `services`, `configmaps`, `secrets`, and `namespaces`—were created first and live inside this core group. They don't have a name in their URL path (e.g., `/api/v1/pods`).

### 2. The Named API Groups (`"apps"`)
```yaml
- apiGroups: ["apps"]
  resources: ["deployments"]
```
* **What it means:** This targets a **Named API group** called `apps`.
* **Why it's used:** As Kubernetes grew, new features were added into separate "packages" or modules so they could be developed independently. Resources that manage application scaling and state—like `deployments`, `daemonsets`, and `statefulsets`—live inside the `apps` group (URL path: `/apis/apps/v1/deployments`).

---

## Common API Groups Reference

When writing RBAC Roles, you must match the resource to its correct group. Here is a quick cheat sheet:

| API Group (`apiGroups`) | Common Resources (`resources`) |
| :--- | :--- |
| **`""`** (Core) | `pods`, `services`, `secrets`, `configmaps`, `persistentvolumeclaims` |
| **`"apps"`** | `deployments`, `statefulsets`, `daemonsets`, `replicasets` |
| **`"batch"`** | `jobs`, `cronjobs` |
| **`"networking.k8s.io"`** | `ingresses`, `networkpolicies` |
| **`"rbac.authorization.k8s.io"`** | `roles`, `rolebindings`, `clusterroles` |

---

## 💡 Pro-Tip: How to find a resource's API Group
If you ever don't know what `apiGroup` a resource belongs to, run this command in your terminal:

```bash
kubectl api-resources
```
Look at the **APIVERSION** column. If it says `v1`, the group is `""`. If it says `apps/v1`, the group is `"apps"`.



The Direct Comparison

- **`apiGroup` (Inside RBAC Rules):** Defines the **logical family** of the resource. It completely ignores version numbers (like `v1` or `v1beta1`) so that your security permissions don't break when Kubernetes upgrades a resource from beta to stable.
- **`apiVersion` (At the top of a YAML):** Defines the **exact schema version** of the manifest you are submitting right now. It tells the Kubernetes API parser exactly how to read the fields in that specific file.


#### Cluster Roles
- SO there are two types of resources, one is namespace-scoped and other is cluster scoped.
  ![[Pasted image 20261008112908.png]]
- For users, for the cluster scoped resources, you use cluster roles and cluster rolebindings.
- Cluster roles are just the roles just they are cluster-scoped.
- ![[Pasted image 20261008113632.png]]
- You can create ClusterRole for the namespaced resouces as well, so when you do that, user will have access to that resource across all namespaces.
- And k8s create some default ClusterRole when the cluster is first setup.
- `kubectl get clusterroles --no-headers | wc -l`
  These kinds of commands are very important manhh, you don't have to calculate manually, there's no chance of errors in there as well.
- kubernetes mai ek ek component acchse se samjhna bhot important hai, understand each and everything properly.


#### Service Accounts:
So there are two types of accounts in the k8s, one is the **User** which is used by the humans and second is the **Service** which is used by the machines, 
![[Pasted image 20261008121312.png]]
For communicating Prometheus or Jenkins to access your k8s cluster, you need authentication, for that we create service account.

A service account is a identity of a service, and is associated with what is known as a token.
A token is what is used for authenticate a service account to the k8s api.

Analogy: Service account is an ID card that we create for a service, the bar code on the Id card is the **token**.

You have one default service account when the cluster is created.

The default serviceaccount has very limited functionality so we create our custom serviceaccount. 

Whenever you create a pod in the cluster, the default service account is automatically attached to that.

![[Pasted image 20261008125035.png]]

Pod is associated with a service account, as soon as it happens, Kubernetes automatically creates a token and mounts that on the pod in some location, and through that the application inside the pod can communicate and make API calls to K8s.

- A **Pod isn’t a machine**; it’s a group of one or more containers running on a node, which is the machine.
- A **ServiceAccount gives the application inside the Pod an identity**, mainly when it communicates with the Kubernetes API. Ordinary communication between applications—such as your backend calling a database—doesn’t require a Kubernetes ServiceAccount.
- Just as a human needs an identity to access the Kubernetes API, an application running inside a Pod uses a ServiceAccount as its identity. RBAC decides what that identity can do.

So basically ServiceAccount acts as an Identity Provider actually.

static Pods, such as kubeadm’s control-plane Pods, don’t use the normal ServiceAccount assignment and token-mounting mechanism.

At times you have to communicate outside the cluster as well like Prometheus/Jenkins or any external application, in that case you can create a token, default validity time is 1hr.
![[Pasted image 20261008130728.png|309]]

![[Pasted image 20261008130815.png]]
decoding the token


So now this token can be used as a authentication to the k8s api, using the bearer token thing.
![[Pasted image 20261008130923.png]]

![[Pasted image 20261008131413.png]]
![[Pasted image 20261008131507.png]]

- `default` Service Account has very limited access.
- The application needs a ServiceAccount with the right permissions to authenticate to Kubernetes.
- The default automatic token mounting mechanism exposes credentials unnecessarily. In the following step, you'll fix this by disabling automatic token mounting on the ServiceAccount and then manually injecting the token into the Deployment using a projected volume. 
  This approach is more secure than the default automatic token mounting because it gives you explicit control over which pods receive API credentials.
- Projected volume: is where the data is coming from.
  Mounted volume: is where it makes the data available at certain path in the container.
![[mermaid-diagram.png|535]]

#### Image security:
For running the private images in the cluster, as we know that its the docker runtime that pulls the image from the registry and all.
So for the private registry, first you have to authenticate with the private registry right, so yeah,

![[Pasted image 20261008155834.png]]
Here `docker-registry` is the built-in secret type that was built for storing Docker credentials only.
regcred is just the name that we have gave.


#### Docker Security and Security Contexts in K8s
Containers are isolated using the namespace in the linux. Docker container can see their own containers or processes only in their namespace.

In Security Context in K8s, we can implement security at the pod level as well as the container level.

So we have two types of root user, one is the host root user, and one is the container level root user,  in the container level root user it has very limited capabilities so that it can disrupt the host machine and other containers running in the namespace. We can add more privileges and capabilities to the container root user by using different commands.
![[Pasted image 20261008231820.png|510]]
You can have security context on the pod level and the container level, applying it to the pod level will apply it to all the containers inside the pod.
and the security context applied to both the levels so at that time container ones override the pod one.

If `runAsUser` is not set at the Pod or container level:
- Image specifies `USER 1000` in its Dockerfile → runs as **UID 1000**.
- Image does **not** specify a user → defaults to **root, UID 0**.

#### Network Policies And Developing Them
![[Pasted image 20261009110304.png|339]]

![[Pasted image 20261009110324.png|375]]
So basically for each component you gonna have ingress and egress rules for the traffic.

In the cluster, any pod can communicate to any pod or service in the cluster by default.
But if you have to restrict access from one particular pod to another particular pod, that's where Network Policy comes, it's also an Object in the K8s just like pod and all, so you attach network policy to the pod. In Network Policy you have certain rules.
We attach Network Policy to Pod using labels and selectors only....
![[Pasted image 20261009112029.png|534]]
![[Pasted image 20261009112254.png|262]]
This `role: db` is the label that is on the db-pod. And this is how it blocks out all the traffic as well.
Always look from this db pod perspective and see what all you need, ingress or egress traffic or both.

And one more thing, if you add ingress, so for the response also you should keep egress right? No!
For the response you don't need a separate rule for that.
So you should be concerned from where does the request originates, you don't need to worry about the response.
As now we have ingress we decide the rules for the ingress....
![[Pasted image 20261009120321.png]]
Its good right by labels and selectors all the similar pods will have the same Network Policy...nice architecture and thinking from the K8s.

But what if the same pods are in the different namespaces?
for the current policy as above it will allow from all the namespaces, but as we only want from the prod namespace, then, 
![[Pasted image 20261009120730.png]]

Even we can connect with the things outside the cluster as well, using the IPBlock.
![[Pasted image 20261009121114.png]]




These two rules have the OR kinda operation.
![[Pasted image 20261009121817.png|238]]

Inside the first one, it has to have both of the conditions true, so kinda AND operation. 
![[Pasted image 20261009121859.png|250]]

But now they are two different rules, so all have the OR condition in between them. 3 Separate rules.
![[Pasted image 20261009122200.png|287]]


Egress Example
![[Pasted image 20261009122527.png|415]]


Actually you have solutions that supports the network policies, this is very important.
So some are there that support that and some are there which doesn't.
![[Pasted image 20261009112511.png|410]]

**DNS Access:**  
DNS is handled by the `kube-dns` service, which listens on port 53 for both UDP and TCP.



### CRD (Custom Resource Definition)
Controller is written in go, and its part of the source code of the K8s.

What is a `custom resource`?  
It is an extension of the Kubernetes API that is not necessarily available in a default Kubernetes installation.

CRD is nothing but just to create our own custom objects in the Kubernetes API.
![[Pasted image 20261009132117.png]]
This is how you create CRD.

Under Schema, openAPIV3Schema is nothing just what you write under the spec section like what all fields are accepted and all.
![[Pasted image 20261009132318.png|331]]
![[Pasted image 20261009132412.png|382]]

But it will just store these things in etcd it won't do anything with it, it doesn't have the controller.
So we have to create a custom controller for this to watch on this.
##### Custom Controllers:
![[Pasted image 20261009135045.png|477]]

Controller is any process or code that runs in a loop and is continuously monitoring the k8s cluster and listening the events of specific objects being changed. 

So you create that custom controller in the go language, clone one sample controller registry from the git and then modify the controller.go file.

Then you can create an image of it, and run it as a container inside pod inside the cluster.

##### Operator Framework
Currently we are first creating the CRD and then creating the custom controller and then deploying. This can be packaged as a whole and deployed using Operator Framework.
![[Pasted image 20261009143132.png]]
By deploying the flight-operator, it internally creates the custom resource definition and also deploys the custom controller as a deployment, an operator does much more than that.
One famous one is the ETCD Operator
![[Pasted image 20261009143505.png|532]]

![[Pasted image 20261009143525.png|509]]

Here is a list of what Kubernetes operators do:

- **Provisioning applications**
- **Managing version upgrades**
- **Scaling workloads automatically**
- **Executing data backups**
- **Restoring data from failures**
- **Monitoring application health**
- **Automating failovers and recovery**
- **Handling configuration changes**
- **Managing external cloud resources**
- **Cleaning up application state**


**More advanced approaches to Kubernetes secrets management**: 
The External Secrets Operator (ESO) is a Kubernetes operator that helps synchronize secrets stored in external secret-management systems-such as AWS Secrets Manager, HashiCorp Vault, Google Secret Manager, and Azure Key Vault-with Kubernetes Secrets. It uses resources such as ExternalSecret, SecretStore, and ClusterSecretStore to define where secrets are stored and how they should be synchronized into the cluster.


## Storage

#### Storage in Docker Containers:
- Storage Drivers
- Volume Driver Plugins
![[Pasted image 20261009160434.png]]
![[Pasted image 20261009160858.png|423]]

the files in the image layer are read-only, and the files in the container layer basically stores the logs generated by the application and all when you run the container, as soon as the container goes down that layer is also gone.
It follows something called as COPY-ON-WRITE mechanism.

![[Pasted image 20261009163141.png|611]]
Its the **Storage Drivers** that do all of this stuff in the docker.

Some common Storage Drivers:
![[Pasted image 20261009163257.png|167]]
Storage Drivers depends on the underlying OS. Docker chooses the best driver available based on the OS.
The different storage drivers also provide different performance and stability
characteristics.


#### Volume Driver Plugins in Docker
So basically, Storage Drivers help manage storage on images and containers. Volumes are not handled by Storage Drivers. Volumes are handled by volume driver plugins.
The default Volume Driver is the `local`.
![[Pasted image 20261009164213.png]]

So basically you can provision volume while running the container.
![[Pasted image 20261009164319.png|303]]


#### Container Storage Interface:
So basically in the past k8s used **containerd** alone as its runtime, and at that time the code with related to the containerd is hardcoded in the k8s source code. 

So as the time passed, many container runtime solutions came like rkt, cri-o etc, so to incorporate that, we have the container runtime interface(CRI), so if any new container runtime comes in the future then it can just follow the CRI principles and get the k8s working with it.

Similarly to extend the support for different networking solutions, the Container Networking Interface(CNI) was introduced, so basically vendors can develop their plugins acc to CNI standards and get it working with k8s.

~lly, we have Container Solution Interface(CSI) to support multiple storage solutions.
And NetApp and Nutanix comes under that, okayy so that's why Nutanix is so heavy infra based manhh.

A **CSI (Container Storage Interface) driver** is ==a standardized, pluggable software component that allows **Kubernetes to seamlessly connect, provision, and manage external storage systems** without hardcoding vendor-specific logic into the core Kubernetes codebase==. 
![[Pasted image 20261010012655.png|493]]

CSI is not k8s specific standard, it is meant to be a universal standard.


So this CSI and storage driver works hand in hand here, like 
![[Pasted image 20261010013338.png]]


In docker, as we attach volume to a container.
In K8s, Basically we attach volume to a Pod.
In volume, you create storage now there are many storage options, same manhh you create one volume and then mount it in the pod using the volumeMounts field.

Now, storage options:
- hostPath, this is not the production way because it is not recommended in the multi-node cluster.
  So we have different cluster storage solutions, 


#### Persistent Volumes:
Now as you are mentioning the storage thing in the pod definition file only but its not the right way in the big production setups, the user has to again and again mention that in the pod definition file......so if any changes that have to made so he has to make changes in each pod.
Instead of that we would like to manage the storage more centrally, where administrator can create large pool of storage and the users carve out pieces from it as required.

That's where PV comes and helps us, its cluster wide.
![[Pasted image 20261010023608.png]]

You select the PV using the Persistent Volume Claims.

![[Pasted image 20261010023900.png|499]]

**Persistent Volume Claim** makes PV available to a pod.

PV and PVC are two different objects in the k8s.
Persistent Volume Claim is bound to a single Persistent Volume.

- **Supply-and-request relationship:** A **Persistent Volume (PV)** acts as the actual storage resource (supply), while a **Persistent Volume Claim (PVC)** acts as the request for that storage.
- **Decoupled infrastructure:** PVs allow administrators to manage the underlying storage hardware, while PVCs allow developers to consume storage without needing to know the technical details of the infrastructure.
- **Strict 1-to-1 binding:** Once the Kubernetes control plane matches a PVC's requirements to an available PV, they bind together exclusively. One PV cannot be shared by multiple distinct PVCs.
- **Pod abstraction:** A Pod does not mount a PV directly; instead, it references a PVC, which acts as the intermediary link to the actual storage.
- **Independent lifecycles:** The PV and its data exist independently of the Pods using them. If a Pod is deleted, the PVC and PV remain intact, preserving the data.

![[Pasted image 20261010024606.png|571]]

![[Pasted image 20261010025155.png]]
![[Pasted image 20261010025210.png]]

![[Pasted image 20261010025428.png]]


Because of portability and security gaps, K8s moved to a newer model.
The modern approach is dynamic provisioning with the StorageClass and CSI drivers.


#### Storage Classes
![[Pasted image 20261010030001.png|687]]

- **Static Provisioning**
**Static provisioning** in Kubernetes means an administrator manually creates a **PersistentVolume (PV)** before an application requests storage.

The user then creates a **PersistentVolumeClaim (PVC)** asking for storage. Kubernetes matches the PVC to a suitable existing PV, and a Pod can use the claim to access that storage.

**Example:** An admin creates a 10 GiB PV backed by a disk. A developer creates a PVC requesting 5 GiB. If the PV’s storage class and access modes also match, Kubernetes can bind the PVC to that PV.
![[Pasted image 20261012111445.png|286]]

**In short:** the storage is set up first; the claim uses what already exists. Dynamic provisioning can create storage automatically when a PVC is created.

- **Dynamic Provisioning**
So for the volumes gets provisioned automatically when an application requires it and that's where StorageClass comes in, so basically, here we define one provisioner such as Google storage that can automatically provision storage on GCP, and attach that to the pod when a claim is made, that's called Dynamic Provisioning of volumes, and you do that using StorageClass object.

So basically what happens, you create StorageClass, as per need you create PVC, and then PVC using the StorageClass creates a volume which is PV using the provisioner, and then binds it with the pod. So, remember it still creates a PV, its just you don't have to create PV manually anymore.
Its created automatically by the StorageClass.
![[Pasted image 20261012112157.png|657]]
we used `gce` provisioner here, there are many others, such as,
![[Pasted image 20261012112651.png|412]]


![[Pasted image 20261012113102.png]]
That's why it is called StorageClass, you can create different classes of Service, next time when you create PVC, you can simply specify the class of Storage you need for the volume.

The Storage Class called `local-path` makes use of `VolumeBindingMode` set to `WaitForFirstConsumer`. This will delay the binding and provisioning of a PersistentVolume until a Pod using the PersistentVolumeClaim is created.


## Networking in K8s

The basics are must on the linux machine.

The switch can only enable communication within a network, 
![[Pasted image 20261012121129.png]]


Router helps connect two networks together.
okayy fine we can send the packets from B to C via router, but how we gonna find the router then?
so there comes the gateway/route. So basically you have to configure things out, and you have to configure it on all the systems actually.
![[Pasted image 20261012121827.png|680]]

Basically you have to add IPs to each system's routing table.
We can have a default gateway as well to route to any network whichever we want if we don't know it.
![[Pasted image 20261012123500.png|696]]

Setting up linux host as a router:
![[Pasted image 20261012123934.png]]

Solution:
![[Pasted image 20261012124149.png]]

in linux, packets are not forwarded from one interface to the next due to security reasons unless you allow them by making an entry, and forwarding related info is at the location, 
![[Pasted image 20261012125041.png|661]]

so these are the important commands, they are working till the restart, if you want to persist these changes, then you have to modify them in the respective system files.
![[Pasted image 20261012125608.png|379]]

#### DNS Configurations:
So basically instead of pinging one system with an IP, if you want to ping them using some name, then you gonna use the DNS, simple.
Actually you can set any hostname on each system in the path `etc/hosts` file which ever you want but its not central right, for different system it can be make different, so we want something central, and managing them as whole is very hard actually.

Translating hostnames to IP addresses this way is known as name resolution.

So, we have the central server now who manages it, we call that DNS server, so all the servers look into that instead of looking into their `etc/hosts` file.

Every host has a DNS resolution configuration file at `etc/resolv.conf`.
But still you can have entries in your host file, so when you don't that entry to be in the DNS server you can have that in the host file, like this Test server.
![[Pasted image 20261012131857.png]]

what if you have an entry in both of the places?
so first it looks at its host file and after that on the DNS server, but that order can also be changed in this file `etc/nsswitch.conf` as shown, 
![[Pasted image 20261012132246.png]]

![[Pasted image 20261012133026.png]]

![[Pasted image 20261012133254.png]]

some knowledge on search option
![[Pasted image 20261012133552.png]]


Record Types: 
![[Pasted image 20261012133842.png]]


Instead of ping you can use nslookup as well, but nslookup does not look into the host entries at `etc/hosts` file. `nslookup` only queries the DNS server.

`dig` is one such another tool.

### Setting one host as the DNS server
In the previous lecture, we saw why you need a DNS server, how it can help manage name resolution in large environments with many hostnames and Ips, and how you can configure your hosts to point to a DNS server. In this article, we will see how to configure a host as a DNS server.

We are given a server dedicated as the DNS server and a set of IPs to configure as entries in the server. There are many DNS server solutions out there; in this lecture, we will focus on a particular one – CoreDNS.

So, how do you get core DNS? CoreDNS binaries can be downloaded from their Github releases page or as a docker image. Let’s go the traditional route. Download the binary using curl or wget. And extract it. You get the coredns executable

`
````
$ curl -LO https://github.com/coredns/coredns/releases/download/v1.12.4/coredns_1.12.4_linux_amd64.tgz
$ tar -zxf coredns_1.12.4_linux_amd64.tgz 
````

Run the executable to start a DNS server. It, by default, listens on port 53, which is the default port for a DNS server.

Now, we haven’t specified the IP to hostname mappings. For that, you need to provide some configurations. There are multiple ways to do that. We will look at one.

First, we put all of the entries into the DNS servers /etc/hosts file. Then, we configure CoreDNS to use that file. CoreDNS loads its configuration from a file named Corefile.

Here is a simple configuration that instructs CoreDNS to fetch the IP to hostname mappings from the file /etc/hosts. When the DNS server is run, it now picks the IPs and names from the /etc/hosts file on the server.

````
.:53 {
    # Use /etc/hosts to resolve hostname
    hosts /etc/hosts {
        reload 1m
        fallthrough
    }

    # Forward unmatched queries to the host's resolver
    forward . /etc/resolv.conf {
       max_concurrent 1000
    }
    cache 30
    log
    errors
}
````

CoreDNS also supports other ways of configuring DNS entries through plugins. We will look at the plugin that it uses for Kubernetes in a later section.

Read more about CoreDNS here:

[https://github.com/kubernetes/dns/blob/master/docs/specification.md](https://github.com/kubernetes/dns/blob/master/docs/specification.md)

[https://coredns.io/plugins/kubernetes/](https://coredns.io/plugins/kubernetes/)

### CoreDNS in Kubernetes



##### Network Namespaces In Linux
![[Pasted image 20261012160102.png]]

![[Pasted image 20261012160925.png]]

![[Pasted image 20261012161113.png]]


In Docker, container and namespace mean the same thing, docker creates a separate network namespace for the container.
![[Pasted image 20261012172213.png|485]]
**Docker Networking**


This is Port Mapping is implemented in the Docker:
![[Pasted image 20261012172521.png]]
![[Pasted image 20261012172537.png]]




When you install **Docker Engine** on a native Linux machine, ==it **uses the host Linux machine directly**== and does not create a virtual machine (VM).
Unlike Windows or macOS—where Docker must first spin up a lightweight Linux virtual machine to run containers—Linux natively supports the technologies Docker relies on.

When you install Docker on Linux:

- **Direct Kernel Sharing:** Docker runs containers as **isolated processes directly on your host's Linux kernel**. There is no guest operating system or virtualization layer.
- **Native Features:** Docker leverages native Linux kernel features like **Namespaces** (for isolation, such as separate network stacks and process trees) and **Control Groups / cgroups** (for resource limiting like CPU and memory limits).
- **Performance:** Because it shares the host hardware and kernel directly without a VM layer, Docker on Linux achieves **near-native performance** and has a significantly smaller resource footprint compared to running it on Windows or Mac.

⚠️ One Important Exception: Docker Desktop for Linux
If you specifically choose to install **[Docker Desktop for Linux](https://docs.docker.com/desktop/setup/install/linux/)** instead of the standard Docker Engine, it **will create a small virtual machine** inside your Linux environment.

The comparison below highlights how these two options behave on a Linux host:

| Feature            | Docker Engine (Standard / Most Common)               | Docker Desktop for Linux                                  |
| ------------------ | ---------------------------------------------------- | --------------------------------------------------------- |
| **Virtualization** | ❌ **No VM**. Runs directly on your host kernel.      | **Yes**. Spins up a lightweight VM.                       |
| **Resource Usage** | Extremely low; utilizes your exact system resources. | Higher; requires dedicated RAM/CPU allocation for the VM. |
| **Interface**      | Command Line Interface (CLI) only.                   | Includes a Graphical User Interface (GUI).                |

**Interfaces carry traffic. Routes tell Linux where to send that traffic.**
**An interface is a network connection point.** It can be a physical adapter or a virtual interface.
![[download (1).png]]

**A route is an instruction in a routing table.** It identifies the destination network, outgoing interface, and—when necessary—the gateway.
br0 is the bridge network.

```
A’s eth0 → host-side veth A → bridge → host-side veth B → B’s eth0
```

![[Pasted image 20261013001834.png]]

Container A’s example routes are:

```
10.10.0.0/24 dev eth0
default via 10.10.0.1 dev eth0
```

|Route|Meaning|
|---|---|
|`10.10.0.0/24 dev eth0`|Reach addresses in this subnet directly through `eth0`|
|`default via 10.10.0.1 dev eth0`|Send destinations without a more specific route through gateway `10.10.0.1`, using `eth0`|

For Container B at `10.10.0.3`, A uses the first route. For an outside address such as `8.8.8.8`, A uses the default route.
**Both use `eth0`, but their next-hop destinations differ.** Routes let Linux make that decision; merely assigning an IP address does not establish every required path.

![[09-how-routes-work.png]]

and yes, container A and B are in the same subnet.

**A veth pair provides the connection across namespace boundaries.** It consists of two linked virtual interfaces: traffic sent through one end arrives at the other.

One end belongs to the container namespace; its peer stays on the host and connects to the bridge.
**`eth0` is the container-side end after renaming.**

| Moment         | Host-side end             | Container-side end                    |
| -------------- | ------------------------- | ------------------------------------- |
| After creation | `veth-a-host` on the host | `veth-a-ns` on the host               |
| After moving   | Still on the host         | `veth-a-ns` inside `netns-a`          |
| After renaming | Still `veth-a-host`       | The same interface, now called `eth0` |
Both ends initially live on the host because we create the pair from the host namespace. Moving one end gives Container A access to it through its own network namespace. Linux also supports creating ends directly in selected namespaces.

The host therefore needs an onward route, IP forwarding, and suitable firewall permissions. **Masquerading** is commonly added when the external network cannot route the container addresses. Creating `br0` alone does not provide all this functionality.

The complete eight-step sequence is:
1. **Create network namespaces:** create separate network views named `netns-a` and `netns-b`.
2. **Create the bridge:** create the shared virtual switch `br0` on the host.
3. **Create veth pairs:** create one virtual cable for A and another for B.
4. **Move the container-side ends:** move them into their respective namespaces and rename each `eth0`.
5. **Attach the host-side ends:** make `veth-a-host` and `veth-b-host` ports on `br0`.
6. **Assign IP addresses:** give A `10.10.0.2/24`, B `10.10.0.3/24`, and the host bridge `10.10.0.1/24`.
7. **Bring the interfaces up:** enable the interfaces so they can carry traffic.
8. **Configure outbound connectivity:** add default routes, enable host forwarding, permit forwarding through the firewall, and configure masquerading where needed.

**A virtual cable is a software connection between two virtual network interfaces.**

A **veth pair** acts like a cable with two connected ends:

|Cable end|Location in our example|
|---|---|
|`eth0`|Inside Container A’s network namespace|
|`veth-a-host`|Inside the host’s network namespace|

A packet sent through `eth0` arrives at `veth-a-host`, and vice versa. Connecting the host-side end to `br0` gives the container a connection to the virtual switch.

**Yes—the eight steps describe Linux networking used in a typical Docker bridge setup.**
    Docker manages these steps automatically. Kubernetes also uses these Linux networking concepts, although the exact setup depends on its networking implementation.

So, there can be the case where pod is running but is not taking the traffic, there could be many reasons, one of them is the readiness checks and therefore be unavailable for normal Service traffic.

**Ingress and Gateway API route incoming application traffic.**
Ingress rules can describe that mapping. An **Ingress controller** reads the rules and configures the infrastructure that handles traffic.

**NetworkPolicies restrict connections between workloads.**
Pods are normally non-isolated in each direction until an applicable policy selects them for that direction.

For a connection between two Pods, the source’s egress restrictions and destination’s ingress restrictions must both permit it. Applicable policies combine their allowed connections; their order does not matter.

A namespace alone does not create a network firewall. Your networking solution must support policy enforcement for NetworkPolicies to take effect.

A Pod calling an external API needs:
1. DNS resolution, if using a hostname.
2. Permission to send traffic.
3. A route out of the cluster.
4. A working return path.

When external networks cannot route Pod addresses, the implementation commonly uses **SNAT** to replace the source Pod IP with a node or gateway address. Return packets are mapped back to the Pod.
![[Pasted image 20261013123516.png]]
So these almost share the same methodology with minor differences. So we can have some standards, and develop solutions that work across runtimes, and that's where CNI(Container Network Interface) comes.

![[Pasted image 20261013124935.png]]

![[Pasted image 20261013125004.png]]

So it comes as kinda plugin.

![[Pasted image 20261013124458.png]]

Docker does not implement CNI, it has something similar called Container Network Model(CNM), 
you can't use Docker with CNI at all.

These Bridge, VLAN and all are the plugins.
And these flannel, cilium and all are the third party ones.

![[Pasted image 20261013124809.png|416]]
k8s create the container in the none network, then invoke the configured CNI plugins who takes care of the rest of the configuration.

  
### Cluster Networking
![[Pasted image 20261013133451.png]]


for multi-master cluster
![[Pasted image 20261013133849.png|509]]


![[Pasted image 20261013134106.png|499]]


some handy commands
![[Pasted image 20261013134205.png]]


#### Few Points:
- So basically you assign IP to the network interface.
	The **`ip a` command** is ==a built-in Linux utility used to **display all network interfaces and their assigned IP addresses**==.

- And you have the MAC address of the interface.
  The `ip link show eth0` command displays the layer 2 (Data Link layer) status and configuration of a specific network interface named eth0. So basically using this command we can get the MAC address of the interface.
  
  This is exactly why the **`ip link`** command exists:
	- It looks specifically at the **Data Link Layer**.
	- Because it targets this layer, its output provides the **MAC address** (labeled as `link/ether`) but completely ignores IP addresses.


- The command **`netstat -nplt`** is used in **Linux** environments to list all active network ports that are currently listening for incoming connections. 
- Correct! That's because `2379` is the port of ETCD to which all control plane components connect to. `2380` is only for etcd peer-to-peer connectivity. When you have multiple controlplane nodes. In this case we don't.


#### Pod Networking in k8s

K8s doesn't have any networking solution to that but expects you to have one, but it lays down some rules that you must be implemented:
![[Pasted image 20261013141513.png]]

  There are networking solutions out there like Cilium, Flannel etc.
  But we can do it on our own as well that gonna help us understand how these solutions do the stuff.
![[Pasted image 20261013141656.png]]

Its bridge interface or networks remember.


![[Pasted image 20261013142348.png]]


For communication of pod in one node to pod in another node.
![[Pasted image 20261013142740.png]]
This is working, but it will get complicated as the networking will get complex.

So the solution is, better do that in a router, so with that the virtual network that we created on each node with 10.244.x.x/24 becomes a single larger network with 10.244.0.0/16.
![[Pasted image 20261013143245.png]]

Lets tie everything together.

So every time the pod is created we will be running a script manually for tieing everything together, but can it automatically run it when the pod is created, so this where CNI comes, 
CNI tells Kubernetes that this is how you should call a script as soon as you create a container.
![[Pasted image 20261013151358.png]]


### CNI in Kubernetes
CNI defines the responsibilities of the container runtimes.

Container runtime is responsible for creating containers, and after that K8s gonna use the appropriate plugins for the networking purposes.

`/opt/cni/bin` this is where the container runtimes see for the plugin, 
`/etc/cni/net.d` but which to use and how to use is configured here.

![[Pasted image 20261013152541.png|482]]

![[Pasted image 20261013152725.png|549]]


![[Pasted image 20261013152902.png|552]]


### ipam(IP Address Management)
In this section we gonna see how the bridge network in the node is assigned the subnet and how are the pods are assigned the IP.
Who stores it? Who assigns it?
![[Pasted image 20261013154520.png]]

![[Pasted image 20261013154707.png]]

CNI comes with two plugins that you can outsource the task to:
![[Pasted image 20261013154929.png]]


### Service Networking
Service is hosted on the cluster, it is not bound to a specific node. Services are a cluster-wide concept.
The service that is only accessible from within the cluster, this type of service is known as ClusterIP.

For outside the cluster, its NodePort, it also works as CLusterIP, as all the pods can access it using its IP.
![[Pasted image 20261013161942.png]]

![[Pasted image 20261013162014.png]]

How are these services getting the IP addresses?
When we create a Service Object in K8s, it is assigned an IP address from a predefined range by K8s.
 ![[Pasted image 20261013162811.png]]
 

kube-proxy sets these IP: Port forwarding.
Ip tables are configured by kube-proxy.

There shouldn't be any case where the pod and the service are assigned the same IP.
![[Pasted image 20261013164007.png]]
 
![[Pasted image 20261013164303.png]]

![[Pasted image 20261013164400.png]]


 The cluster CIDR is the large master pool of IP addresses, and ==every individual pod's IP address is assigned directly from a smaller slice (sub-block) of that pool==.

How the Relationship Works

- **The Cluster CIDR (The Big Pool):** This is the overarching network range (for example, `10.42.0.0/16` in K3s or `10.128.0.0/14` in OpenShift) defined at the cluster level. It represents the total amount of space reserved strictly for pod networking.
- **Node Subnet Allocation (Slicing the Pool):** The Kubernetes controller manager or your CNI (Container Network Interface) plugin breaks the cluster CIDR into smaller chunks—often called a _Pod CIDR_ or _Host Prefix_ (such as a `/24` or `/23`)—and assigns one chunk to each worker node.
- **Pod IP Assignment (Individual IPs):** When a pod is scheduled onto a specific node, the node’s local CNI daemon picks an unused IP address from that node's assigned sub-range. Because every node's sub-range is carved out of the main cluster CIDR, every single pod IP naturally falls inside the cluster CIDR range.

**Kubernetes Service IPs are not allocated from the Cluster CIDR.** Instead, ==they are allocated from a completely separate, dedicated range called the **Service CIDR**== (often configured via the `--service-cluster-ip-range` flag).


Here is how the two ranges differ and why they are kept separate:

The Difference Between the Ranges

|Network Feature|Allocation Source|Characteristics|
|---|---|---|
|**Pod IPs**|**Cluster CIDR**|Real, routable IP addresses assigned to network interfaces on individual containers.|
|**Service IPs (ClusterIP)**|**Service CIDR**|"Virtual" or "fake" IPs that do not belong to any physical or virtual network interface.|

Why Service IPs are Different

- **They are Virtual:** A Service IP (ClusterIP) exists only as a load-balancing rule in the Linux kernel (handled by `kube-proxy` using IPVS or iptables, or by eBPF in Cilium). Traffic sent to a Service IP is intercepted instantly on the host node and redirected straight to a backend Pod IP.
- **Preventing IP Conflicts:** If Services and Pods shared the same CIDR pool, the cluster could accidentally assign the exact same IP address to both a virtual service router and a physical container interface, breaking network routing entirely.


### Cluster DNS in K8s
When the service gets created, kubeDNS automatically creates an entry of it by default, but not for the pods by default but we can enable that explicitly. 
![[Pasted image 20261013171725.png]]
They are all in the same default namepace, so they can just call their name like web-service and reach out.

With different namespace:
![[Pasted image 20261013172155.png]]


All the services are further grouped together into another subdomain called svc.
And finally all the services and pods are grouped together into a root domain for the cluster, which is set to cluster.local by default.
![[Pasted image 20261013172522.png]]


for pods:
![[Pasted image 20261013172813.png]]

![[Pasted image 20261013172840.png]]



### CoreDNS: How K8s Implements DNS

The core-dns is deployed as the pod in the kube-system namespace in the k8s cluster.
When you deploy the core dns, it deploys a service with it, so that pods can reach the core-dns using that service.

actually whenever you want to know/find/debug anything just describe pods/service/deployment, you will get.


## Ingress

  
![[Pasted image 20261014132053.png|505]]

![[Pasted image 20261014132110.png|513]]

without ingress, you are just introducing one lb after another so it increases your cloud cost, and you configure TLS at the load balancer level.



![[Pasted image 20261014133012.png]]
so basically if you add one another service then again one another load balancer and all, maintaining them and the cloud cost all increases.

So wouldn't be nice to configure all of that in the k8s cluster only, and all those configuration just another k8s definition file that lives along with the rest of the application deployment files, that's where Ingress comes in.

Ingress helps your users access your application using a single externally accessible URL that can configure to route traffic to different services within your cluster based on the URL path. At the same time, implement SSL security as well.

![[Pasted image 20261014135522.png]]
Think of Ingress as a layer seven load balancer built into the k8s cluster.

So basically you are replacing all the load balancers with just one externally accessible URL that's it, in that way you are lowering your cost as well and less configuration to manage and smarter way to handle.


Creating Ingress Controller.
![[Pasted image 20261014134927.png]]


Creating service to expose this Ingress Controller Deployment.
![[Pasted image 20261014135341.png]]

Nginx Controller do just more than load balancing as well so basically you have to configure and add permissions to it, so you have to add Service Accounts as well.
![[Pasted image 20261014135454.png]]


In the ConfigMap, we pass on the Ingress configuration data.

Summary
![[Pasted image 20261014135657.png]]


Ingress Resource:
![[Pasted image 20261014135759.png]]


![[Pasted image 20261014135921.png]]

![[Pasted image 20261014135948.png|459]]

![[Pasted image 20261014140302.png]]

All they can be pointed to the same Ingress Controller service, just have to make all the DNS entries.
![[Pasted image 20261014140828.png]]
![[Pasted image 20261014140845.png]]

So first you have rules, and under each rule you can have different paths.

![[Pasted image 20261014141039.png|650]]


By domain names/host names:
![[Pasted image 20261014141414.png]]

Just a comparison:
![[Pasted image 20261014141441.png]]

![[Pasted image 20261014151234.png]]


Different ingress controllers have different options that can be used to customise the way it works. NGINX Ingress controller has many options that can be seen [here](https://kubernetes.github.io/ingress-nginx/examples/). I would like to explain one such option that we will use in our labs. The [Rewrite](https://kubernetes.github.io/ingress-nginx/examples/rewrite/) target option.

Our `watch` app displays the video streaming webpage at `http://<watch-service>:<port>/`

Our `wear` app displays the apparel webpage at `http://<wear-service>:<port>/`

We must configure Ingress to achieve the below. When user visits the URL on the left, his/her request should be forwarded internally to the URL on the right. Note that the /watch and /wear URL path are what we configure on the ingress controller so we can forward users to the appropriate application in the backend. The applications don't have this URL/Path configured on them:

`http://<ingress-service>:<ingress-port>/watch` --> `http://<watch-service>:<port>/`

`http://<ingress-service>:<ingress-port>/wear` --> `http://<wear-service>:<port>/`

Without the `rewrite-target` option, this is what would happen:

`http://<ingress-service>:<ingress-port>/watch` --> `http://<watch-service>:<port>/watch`

`http://<ingress-service>:<ingress-port>/wear` --> `http://<wear-service>:<port>/wear`

Notice `watch` and `wear` at the end of the target URLs. The target applications are not configured with `/watch` or `/wear` paths. They are different applications built specifically for their purpose, so they don't expect `/watch` or `/wear` in the URLs. And as such the requests would fail and throw a `404` not found error.

To fix that we want to "ReWrite" the URL when the request is passed on to the watch or wear applications. We don't want to pass in the same path that user typed in. So we specify the `rewrite-target` option. This rewrites the URL by replacing whatever is under `rules->http->paths->path` which happens to be `/pay` in this case with the value in `rewrite-target`. This works just like a search and replace function.

For example: `replace(path, rewrite-target)`

In our case: `replace("/path","/")`

```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: test-ingress
  namespace: critical-space
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
    - http:
        paths:
          - path: /pay
            pathType: Prefix
            backend:
              service:
                name: pay-service
                port:
                  number: 8282
```

In another example given [here](https://kubernetes.github.io/ingress-nginx/examples/rewrite/), this could also be:

`replace("/something(/|$)(.*)", "/$2")`

```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: rewrite
  namespace: default
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /$2
spec:
  rules:
    - host: rewrite.bar.com
      http:
        paths:
          - path: /something(/|$)(.*)
            pathType: Prefix
            backend:
              service:
                name: http-svc
                port:
                  number: 80
```


FEW IMPORTANT THINGS HERE:
1. The port number should match the port the service is open to, so see the service.
2. Use the service name properly.
3. `Ingress` resource is not `Pod`!!!!! use commands properly.
4. And `Ingress` resource is namespace scoped.


The NGINX annotation:

```
nginx.ingress.kubernetes.io/rewrite-target: /
```

rewrites the matched request path to `/` before sending it to the service. So the backend receives `/` rather than `/pay` or `/pay/orders`.

That behavior is specific to the NGINX Ingress controller; the annotation is not part of the core Kubernetes Ingress API.


### Gateway API
So as we have two services but we have the single ingress resource that is being used to manage both the resources, 

Its an official k8s project focussed on layer 4 and layer 7 routing.

![[Pasted image 20261014165659.png]]


![[Pasted image 20261014165958.png]]


![[Pasted image 20261014170111.png]]
annotations are very specific to the underlying controllers...and k8s is itself not aware of these configurations as they are underlying controller based so it can't validate if they are right or wrong. 

And this is where Gateway API comes in, it focuses on Layer 4 and Layer 7 routing.
![[Pasted image 20261014170502.png]]

![[Pasted image 20261014170618.png]]
We have three different personas here, 

![[Pasted image 20261014170701.png]]
we have routes other than HTTPRoute only...

![[Pasted image 20261014170920.png]]

![[Pasted image 20261014171051.png]]




Differences: See how clear and easy to understand Gateway API provides, and see no confusing and vendor lockin kinda annotations needed.
![[Pasted image 20261014171654.png]]


See here vendor specific thing in the Gateway API, so it will work across all the Gateway API Implementation.
![[Pasted image 20261014171915.png]]


Actually Gateway API breaks the vendor lockin kinda syntax and things, and is more self-explanatory and easy to understand.

![[Pasted image 20261014172149.png]]


![[Pasted image 20261014172239.png]]

In Gateway API as well you have to give the provider, its just the code and all, overall the method is so clean and good!

To use the **Gateway API**, a **controller** is required.


------

`apiVersion: gateway.networking.k8s.io/v1`
`kind: Gateway`
`metadata:`
  `name: nginx-gateway`
  `namespace: nginx-gateway`
`spec:`
  `gatewayClassName: nginx  # Replace with your controller class (e.g., istio, envoy-gateway, traefik)`
  `listeners:`
    `- name: http`
      `protocol: HTTP`
      `port: 80`
      `allowedRoutes:`
      `# Allows routes from any namespace; use "Same" to restrict to this namespace`
        `namespaces:`
          `from: All` 
`

so by this we are creating this Gateway resource in the nginx-gateway namespace but we are allowing routes from services from all the  namespaces right?


Ans: Yes, the `Gateway` resource is created in the `nginx-gateway` namespace.

`allowedRoutes.namespaces.from: All` allows **Gateway API route resources**—such as `HTTPRoute`—from any namespace to attach to this listener, as long as they also match the listener’s other rules.

It does **not** directly allow Services from every namespace. An `HTTPRoute` usually references a Service in its own namespace; the route then sends traffic to that Service.


----------

`apiVersion: gateway.networking.k8s.io/v1`
`kind: HTTPRoute`
`metadata:`
  `name: frontend-route`
  `namespace: default`
`spec:`
  `parentRefs:`
    `- name: nginx-gateway`
      `namespace: nginx-gateway`
      `sectionName: http`
  `rules:`
    `- matches:`
        `- path:`
            `type: PathPrefix`
            `value: /`
      `backendRefs:`
        `- name: frontend-svc`
          `port: 80`


here, `sectionName` is the listener that is very important to mention, and also the namespace of where the gateway has been placed.

-----------

### Designing a Kubernetes Cluster
The nodes forming a K8s cluster can be physical and virtual.

basically all the containers and k8s all works over the linux machine only, it can be small as well........
![[Pasted image 20261015234212.png]]

![[Pasted image 20261015234232.png]]

![[Pasted image 20261015234304.png]]

There are many other solutions as well in each category.

if the master node goes down you can't do anything!! can't even run a single kubectl command as if goes through the Kubeapi-server, so that's why we say to have 2 master nodes for HA.

Understand how two nodes in the cluster works.

When an request comes, it is processed only once, see the image for reference:
![[Pasted image 20261016000914.png]]

so basically we have to load balancer that is receiving this request, and it splits the traffic between the API servers, 

What about Schedulers and control managers? 
They might duplicate in actions resulting in more pods than actually needed right!  So they must not run in parallel right, they work in Active, Standby mode. how it is achieved like which is in active or standby mode? Through the Leader Election Process.

![[Pasted image 20261016002115.png]]

![[Pasted image 20261016002208.png]]


There are two ways to setup etcd server, one is Stacked Technology where you have the etcd in the control plane nodes. Here the failed control plane node will risk the etcd server.
![[Pasted image 20261016003444.png]]
Other is External Etcd server, where etcd is separated from the control plane node.
again, API server is the only component that talks to the etcd server.
![[Pasted image 20261016004735.png]]
here in this we need to make sure that the API server is pointing to the etcd server.
![[Pasted image 20261016004935.png]]

etcd is a distributed server so that's why we have mentioned the list of the servers.

For HA, you have to keep multiple master nodes! And that load balancer is also a node.
![[Pasted image 20261016005336.png|435]]
total of 5 nodes in a cluster.

## etcd in HA

1. etcd
2. Key value store
3. how we operate etcd
4. RAFT protocol
5. best practises for number of nodes

etcd and Quorum.
And why we should have odd number of nodes, and why not even because it makes it go out of Quorum.

![[Pasted image 20261016134059.png]]

![[Pasted image 20261016135232.png]]


![[Pasted image 20261016135303.png]]
so for High HA we atleast need 3 master nodes.
Also we go for the stacked topology, ie. etcd on the master node itself.



Installing Kubernetes the hard way can help you gain a better understanding of putting together the different components manually.

An optional series on this is available on our YouTube channel here:

[https://www.youtube.com/watch?v=uUupRagM7m0&list=PL2We04F3Y_41jYdadX55fdJplDvgNGENo](https://www.youtube.com/watch?v=uUupRagM7m0&list=PL2We04F3Y_41jYdadX55fdJplDvgNGENo)

The GIT Repo for this tutorial can be found here: [https://github.com/mmumshad/kubernetes-the-hard-way](https://github.com/mmumshad/kubernetes-the-hard-way)


## Setting up k8s cluster using kubeadm and in local environment

So this is all we are building it in our local environment.
![[Pasted image 20261016140029.png]]

The kubeadm basically helps us bootstrap all the k8s components in the right node in the right order.


The vagrant file used in the next video is available here:

[https://github.com/kodekloudhub/certified-kubernetes-administrator-course](https://github.com/kodekloudhub/certified-kubernetes-administrator-course)

Here’s the link to the documentation:

[https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/)


Vagrant is an open-source tool used ==to build, configure, and manage reproducible, portable virtual machine (VM) development environments==. [1, 2]

## What Vagrant Does

- Eliminates "It works on my machine": It allows teams to share identical development environments so that code runs the same way on every developer's computer, regardless of their host operating system (Linux, macOS, or Windows). [1, 3, 4]
- Automates Environment Setup: Instead of manually installing software, setting up networking, or configuring dependencies, you define everything inside a single text file called a Vagrantfile. [3, 4, 5]
- Controls Virtualization Providers: Vagrant acts as a simple wrapper or command-line interface sitting on top of hypervisors and cloud platforms like Oracle VirtualBox, VMware, Hyper-V, Docker, or AWS. [1, 5, 6]
- Manages the VM Lifecycle: You can spin up, configure, pause, and delete entire virtual machines using simple terminal commands like `vagrant up`, `vagrant ssh`, `vagrant halt`, and `vagrant destroy`. [2, 7, 8]
- Supports Automated Provisioning: It integrates with configuration management and scripting tools like Shell scripts, Ansible, Chef, and Puppet to automatically install databases, web servers, or runtimes upon boot. [1, 4, 5]

If you'd like, let me know what kind of project you are working on, and I can help you write a basic Vagrantfile or guide you through the setup steps.

Still Virtual Box is our hypervisor, responsible for running our virtual machines.
So Vagrant is basically an automation tool, used for spinning up whole set of VMs with specific configuration.

----

Yes, that’s basically right. **Vagrant automates creating and configuring development environments**, often by using a provider such as VirtualBox.

You write a **Vagrantfile** describing the VM (for example, its OS image, CPU, memory, and setup steps). Vagrant then asks VirtualBox to create and start it, and can run provisioning scripts to install and configure software inside it.

So: **Vagrant coordinates the automation; VirtualBox provides the VM.** Vagrant can also use other providers, such as VMware or cloud providers.

So actually you need a good little high end system to do all of this stuff. 

---
So basically after this we have all the nodes ready, now we gonna install kubeadm for setting up the k8s cluster.

for high HA, you need 2 master nodes.

As the k8s is container runtime agnostic, so manually we have to install the container runtime like containerd or so.

- now you gonna install the cgroups which basically allows you to specify resource limits on your containers.
- in the containerd section, some config file, you have to make some crgroup setting to True.
- There are various other flags that we have to pass and all.
- so basically for the networking and all, you have to do all of those stuff, connecting interfaces and all.
- And actually you have to check with some CNI plugin as well like Flannel or Cilium.
- Basically you can just install it, it provides a manifest file of its own and through that you can just install it.
- we first have to setup the master node and after that basically you join the worker nodes to the cluster.


testing functionality and regression testing

Functional requirement.
it should 



























------------





Make a list of startups that you wanna/can go for manhh!!!!

And a list of good companies, keep watching them, as soon as the opening is there, just dm the co-founder and all, so just get into startups manhh.


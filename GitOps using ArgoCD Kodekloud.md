# GitOps using ArgoCD


### Intro

Actually you have to understand the relation and how to use all the things together as well...
like the ArgoCD, CI/CD pipeline and Helm.

<img width="384" height="289" alt="image" src="https://github.com/user-attachments/assets/fe7c2836-18c5-454b-91ff-5b0f9fdba72a" />
these basically reduces the manual effort of doing things...

So the traditional CD is the push-based approach that we have used earlier in our projects like using kubectl command to push changes
to the k8s cluster.
Basically for all the infra related things related to K8s you are still doing things manually running the kubectl commands and all.

And as we do apply CLI commands and apply changes then the configuration in the git is not the latest.
<img width="1906" height="981" alt="image" src="https://github.com/user-attachments/assets/7b0e00e2-d9de-4e3b-b31a-285170007e6d" />

So you have to remember as well what all changes that you have done manually using the CLI.
So this is the problem that GitOps solve.

#### What is GitOps?
In GitOps, the entire code delivery process is controlled via git.

<img width="1740" height="967" alt="image" src="https://github.com/user-attachments/assets/e31a387b-6f29-4d1d-988a-656ca80294c7" />

You remember right how in the first POC we have created all the K8s manifest files in the cluster only and no git and all was there.
But here you have everything infra, application code, and k8s manifest in the git repo.

Yes you have the K8s manifest file in one git repo, not just we created in the cluster and applied there so you can see right
how much we have to remember so many stuff regarding what all we have commands and configuration that we have applied right.

GitOps operator runs in one of the k8s cluster, and can push changes to other cluster as well.
<img width="1733" height="957" alt="image" src="https://github.com/user-attachments/assets/7dc60496-cc8e-4391-8108-aef338b6ccb9" />

---

### GitOps Principles
1. Declarative over Imperative: GitOps uses Declarative way, so this we have the state as well right!
2. Make use of git.
3. The desired state can be applied in one or more environments or clusters.
4. Reconcilation
<img width="1864" height="950" alt="image" src="https://github.com/user-attachments/assets/c3d9cc19-c068-4813-a3bf-0196c42ec71b" />

### GitOps vs DevOps

GitOps is primarily used with containerization technologies like OpenShift or Kubernetes, while DevOps can be used with application.
In GitOps its essential to have two git repos, one for the application code and other for the other for the kubernetes manifest files.

So the changes are pulled by the Operator in the GitOps, in DevOps changes are pushed to the cluster.

<img width="1916" height="971" alt="image" src="https://github.com/user-attachments/assets/bd5d7e9a-fdad-4cf7-bc3a-8ab2a2d5dc3f" />


### Push vs Pull Based Deployments














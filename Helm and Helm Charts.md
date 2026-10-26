# Helm and Helm Charts

<img width="1742" height="942" alt="image" src="https://github.com/user-attachments/assets/d9c05d62-cbc5-4978-8ac6-e9552d99698a" />

So helm is basically a package manager, instead of maintaining each and every YAML file on your own for the whole application, we can use helm for managing that, simple as that.

#### Helm Components
Charts are a collection of files, and they contain all the instructions that Helm need to know to be able to create the collection of objects that you need in your k8s cluster.

When a chart is applied to your cluster, a release is created.
Each release can have multiple revision. Each release is like a snapshot of the application.
Actually the whole point of having multiple releases is that we can have multiple releases of the same chart. So they can be tracked separately and changed independently...
Even they are based out of one chart, they are entirely two different entities.
Use case is that you can have suppose one instance of Wordpress website that is visible to your customers, and another instance of the same website visible to your internal team of developers, there they can add new features and test the website.
<img width="1860" height="726" alt="image" src="https://github.com/user-attachments/assets/77782ae3-426d-4a70-890a-59edc6e21ef0" />


Helm stores the meta data in the Kubernetes Secrets.

Actually you already have so many templates available, most of the times, all you need is just to modify the values.yaml file that's it...

Thousands are charts are already available at different helm repos...
<img width="1209" height="783" alt="image" src="https://github.com/user-attachments/assets/21656399-0391-4e94-9144-84e80b5515e9" />



---
Bro just lock the fk in, learn devops and SRE related stuff, and prepare for interview and all and just switch from this company...and probably work for US/Global companies manhh!!!

And also once you learn about these things, start to build something on your own, some deep-tech related startup with related to engineering and stuff manhh!!! Be a deep tech founder!!!
Like you have CastAI, vCluster, these kinda things actually!!!!

Start building manhh, keep learning and keep applying, and keep building these deep-tech startups!!!!!

And one more thing, either late nights or early mornings...........simple as that manhh, study at that time onlyyyyyyyyy!!!! there's max focus at this time!!!!

Go all in tech, and build these deep tech startups, earn or raise money, get money and exit, simple as that, then start building some other one!!!!!!!!!!!!

And if you have anything like that in the market, still make that with more refinement and good features actually!!! All products have the market manhhh!!!

I want to be deep tech startup founder manhh, like of CastAI or vCluster, so with related to K8s and infra related stuff only actually......

-------------

#### Helm Charts
Helm basically knows how to do its job using charts actually. Charts are kinda intruction manuals for it.

<img width="1713" height="875" alt="image" src="https://github.com/user-attachments/assets/56a3a126-8d81-48ab-bbdd-5cb0be4057e3" />

This is basically called templating, and as we can see we get the values from the values.yaml to create the final version to deploy it on Kubernetes.
Chart.yaml has the information related to the chart.


<img width="1267" height="789" alt="image" src="https://github.com/user-attachments/assets/9a6f94f1-e330-4494-9313-71ec772fbb05" />

This apiVersion is introduced in the Helm 3, so to distinguish between the chart built on Helm 2 and Helm 3.

appVersion is the version of the application that's inside of this chart. In this case, suppose the application is the WordPress. So it will deploy 5.8.1 version of the application.

version is the version of the chart itself. And this is independent of the app that this chart will deploy.

So there are two types of charts, application and Library.

Dependencies are basically what it depends on, like it has its own charts like here there is MariaDB dependency...

Keywords are just used for searching for the repo in the public chart repository.

<img width="1287" height="929" alt="image" src="https://github.com/user-attachments/assets/5183b6ea-7994-4738-a758-7d5510c1b461" />

<img width="1806" height="933" alt="image" src="https://github.com/user-attachments/assets/a11ee0c2-85a4-42de-800e-fe0f11c07503" />



#### Helm Basics
<img width="1850" height="782" alt="image" src="https://github.com/user-attachments/assets/a4729bc4-9025-481d-96e6-955ee64e3868" />


Helm release management is one thing!!!!

So helm is nothing just the package manager like npm, how when you install some node package using npm you don't install all the related files and all right one by one, you just run the npm install --dashhhhhh command right and it gets installed, that's how the helm is, you run helm add command and it installs the package of the application in the cluster that's it, and in that package you have several k8s objects files, similarly if we want to remove the package or the application we can just helm uninstall it and it will remove the application/all the related K8s objects related to that application.

***Helm helps when you want reusable templates, configuration for different environments, and release management such as upgrades and rollbacks. For a small or straightforward app, plain YAML with `kubectl apply` can work well.***

### Customizing Chart parameters
<img width="1853" height="992" alt="image" src="https://github.com/user-attachments/assets/2ee170a8-0113-4a2f-831b-40f56db50b8f" />

<img width="1892" height="831" alt="image" src="https://github.com/user-attachments/assets/61c82b7e-dbcf-4160-9d9f-2720cb4ba285" />

<img width="1816" height="428" alt="image" src="https://github.com/user-attachments/assets/40754a36-088f-4942-8706-818bb38c2a09" />

<img width="1851" height="904" alt="image" src="https://github.com/user-attachments/assets/9a8249b2-f8a8-4876-bb4b-8d1cd68fc286" />


`my-release` is just a **placeholder name** for a Helm release. It’s the name you choose to identify one installed instance of a chart.

For example:

```
helm install swiftpay ./swiftpay-chart
```

Here, `swiftpay` is the release name. You’d use it in commands such as:

```
helm status swiftpay
helm upgrade swiftpay ./swiftpay-chart
helm uninstall swiftpay
```

You can choose another name, like `dev`, `payments-prod`, or `my-release`. The chart is the package being installed; the release name identifies that particular installation.

---
### Bitnami helm charts

A **Bitnami Helm chart repository** is a place where Bitnami publishes Helm charts—prepackaged Kubernetes templates for applications such as PostgreSQL, Redis, and Kafka.

You can add a chart repository to Helm with:

```
helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo update
```

Then install a chart from it, for example:

```
helm install my-redis bitnami/redis
```

Here:

- `bitnami/redis` means the **Redis chart** from the **Bitnami repository**.
- `my-redis` is the **release name** for this installation in your cluster.
- Helm reads the chart and creates or updates the Kubernetes objects it defines.

One distinction: the chart repository stores the **chart package**; the application’s container image is pulled separately by the Kubernetes nodes.

--

In this command:

```
helm repo add bitnami https://charts.bitnami.com/bitnami
```

- `helm repo add` tells Helm to **save a chart repository** so you can use charts from it.
- `bitnami` is the **local nickname (alias)** you choose for that repository.
- `https://charts.bitnami.com/bitnami` is the repository’s URL.

After adding it, you can refer to a chart using that nickname:

```
helm install my-redis bitnami/redis
```

Here, `bitnami/redis` means “the chart named `redis` from the repository I saved under the nickname `bitnami`.” You could choose another nickname when adding the repo, but `bitnami` is commonly used for Bitnami’s chart repository.

---

### Common Helm Commands

Here are the Helm commands you’ll use most often. In these examples, `myapp` is the **release name**, and `./my-chart` is the path to a chart.

#### Add and find charts

```
helm repo add bitnami https://charts.bitnami.com/bitnami
```

Adds a chart repository and gives it the local nickname `bitnami`.

```
helm repo update
```

Refreshes the list of charts and versions available from your added repositories.

```
helm search repo bitnami
helm search repo bitnami/redis
```

Searches your added repositories for charts.

#### Install and inspect

```
helm install myapp ./my-chart
```

Installs a chart as a release named `myapp`.

```
helm list
helm list -n production
```

Lists Helm releases in the current namespace, or in `production`.

```
helm status myapp -n production
```

Shows the release’s status and related information.

```
helm get values myapp -n production
```

Shows the values used by the release.

#### Upgrade, rollback, and uninstall

```
helm upgrade myapp ./my-chart -n production
```

Updates an existing release using the chart and its values.

```
helm upgrade --install myapp ./my-chart -n production
```

Upgrades `myapp` if it exists; otherwise, installs it.

```
helm history myapp -n production
```

Shows the release’s revisions.

```
helm rollback myapp 1 -n production
```

Rolls the release back to revision `1`.

```
helm uninstall myapp -n production
```

Uninstalls the release and its Helm-managed resources.

#### Work with chart files

```
helm show values bitnami/redis
```

Displays a chart’s default configuration values.

```
helm template myapp ./my-chart
```

Renders the chart into Kubernetes YAML locally without installing it.

```
helm lint ./my-chart
```

Checks a chart for common errors.

For example, a typical install might look like:

```
helm install myapp ./my-chart \
  --namespace production \
  --create-namespace \
  -f values-prod.yaml
```

This installs the chart as `myapp` in the `production` namespace, creates that namespace if needed, and applies settings from `values-prod.yaml`.

---
### Lifecycle management with Helm

Basically if we want to update something, then with related to that we have to update all of the other k8s objects right in the release, that's where it gets very hard, and that's where helm comes into the picture and with just the one helm command you can do that stuff, helm will take care of the rest.

Basically helm keeping track of the current state, previous state and bringing it into the future states.


---

### Helm rollback and revisions

A Helm release keeps a **history of revisions**. Each install or upgrade creates a new revision containing that release’s configuration and the chart used for it.

Suppose the release history is:

| Revision | Configuration          |
| -------- | ---------------------- |
| 1        | Image `v1`, 2 replicas |
| 2        | Image `v2`, 3 replicas |

If you run:

```
helm rollback myapp 1
```

Helm **does not erase revision 2 or move the release history backward**. It takes the configuration from revision 1 and applies it again as a **new revision**—revision 3.

| Revision | Configuration          |
| -------- | ---------------------- |
| 1        | Image `v1`, 2 replicas |
| 2        | Image `v2`, 3 replicas |
| 3        | Image `v1`, 2 replicas |

So revision 3 has the same configuration as revision 1, but it is a new revision created by the rollback. The history stays available for inspection:

```
helm history myapp
helm status myapp
```

You can also roll back to the previous revision without specifying its number:

```
helm rollback myapp
```

**In short:** rollback reapplies an earlier release configuration and records that action as a new revision.

---

### Chart version and App version

A Helm chart has two different version fields:

- **Chart version (`version`)**: the version of the chart package—its templates and default configuration.
- **App version (`appVersion`)**: the version of the application the chart is intended to deploy, often matching its container image version.

For example, a chart might contain:

```
# Chart.yaml
version: 2.4.1
appVersion: "16.3.0"
```

This means **chart version 2.4.1** packages the Kubernetes configuration, and it is intended to deploy **application version 16.3.0**.

They can change independently. A chart update might fix a Deployment template without changing the app version. Conversely, the chart can be updated to deploy a newer app version. The actual image tag is configured by the chart’s values and may not always match `appVersion`, so check the chart configuration to confirm what image gets deployed.


---

## Helm upgrades, database backups, and hooks

A Helm rollback restores the **Kubernetes resources and release configuration** from an earlier revision. It does **not automatically restore data stored outside those resources**, such as records in an external database, files in object storage, or data on a persistent volume.

For example, an upgrade might change the app to expect a new database schema. Rolling back the Helm release can restore the old app version, but it does not automatically undo database migrations or recover database data that was changed or deleted.

### Plan database backups separately

Before an upgrade that could affect data, use a backup process appropriate for that database:

1. Take a database snapshot or logical backup.
2. Confirm the backup completed and can be restored.
3. Apply the chart upgrade.
4. Keep the backup until the upgraded application is verified.

A persistent volume is not automatically a backup. It may preserve data when a Pod is replaced, but it does not protect against every failure or destructive change.

### Can chart hooks take the backup?

Yes. A chart can define a **pre-upgrade hook** that runs a Kubernetes Job before Helm updates the chart’s normal resources. That Job could call a backup script or a database backup tool.

A simplified example:

```
apiVersion: batch/v1
kind: Job
metadata:
  name: myapp-db-backup
  annotations:
    "helm.sh/hook": pre-upgrade
spec:
  template:
    spec:
      restartPolicy: Never
      containers:
        - name: backup
          image: example/backup-tool:1.0
          command: ["sh", "-c", "run-database-backup"]
```

For this to work, the Job needs the right database access, credentials, storage destination, and error handling. Helm waits for hook Jobs to complete, so a failed backup Job can stop the upgrade.

### Important limits

- A hook is only useful if the chart author or operator has configured it. Helm does not create backups automatically.
- Hooks have lifecycle and cleanup rules; a completed hook Job may be deleted depending on its annotations.
- A backup hook does not guarantee the backup is restorable. Verify backups and practice restores.
- Restoring data is a separate operation. A Helm rollback does not automatically run a database restore hook.

**Practical rule:** use hooks to coordinate a backup with an upgrade when appropriate, but rely on a tested database backup and recovery process for data protection.


---

### Writing your own Helm Chart
Apart just from installing the application via these charts, it can do other many stuff as well!!
Such as the backup and restore of the data from the database/volumes...

Basically Helm Chart is a directory with a specific structure with the templates directory and the other supporting files like the values.yaml, Chart.yaml, License etc.

**Helm Directory Structure** 

```text
hello-world-chart/
├── templates/
├── values.yaml
├── Chart.yaml
├── LICENSE
└── README.md
```


##### `templates/service.yaml`

```yaml
apiVersion: v1
kind: Service
metadata:
  name: hello-world
spec:
  type: NodePort
  ports:
    - port: 80
      targetPort: http
      protocol: TCP
      name: http
  selector:
    app: hello-world
```

##### `templates/deployment.yaml`

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hello-world
spec:
  replicas: 2
  selector:
    matchLabels:
      app: hello-world
  template:
    metadata:
      labels:
        app: hello-world
    spec:
      containers:
        - name: hello-world
          image: nginx
          ports:
            - name: http
              containerPort: 80
              protocol: TCP
```

Basically when you install a chart, it installs the chart and creates the deployment.

We should not have hardcoded or static values in the Deployment or the Service file.
For that we use Helm templating language so every time we create a new release it should not give us any errors or so....

## Templatize

Install the chart with the release name `hello-world-1`:

```bash
helm install hello-world-1 ./nginx-chart
```

In the Deployment template, use `{{ .Release.Name }}` to include the Helm release name in the resource name:

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: {{ .Release.Name }}-nginx
spec:
  replicas: 2
  selector:
    matchLabels:
      app: hello-world
  template:
    metadata:
      labels:
        app: hello-world
    spec:
      containers:
        - name: hello-world
          image: nginx
          ports:
            - name: http
              containerPort: 80
              protocol: TCP
```

With the release name `hello-world-1`, the Deployment is named `hello-world-1-nginx`.

<img width="1726" height="772" alt="image" src="https://github.com/user-attachments/assets/37599836-b718-43f1-aeb4-9278f73afac8" />

<img width="1856" height="815" alt="image" src="https://github.com/user-attachments/assets/3ecb07f3-ba43-4b52-9815-f5c60868b310" />

Helm does not allow two releases with the same name.

<img width="1786" height="944" alt="image" src="https://github.com/user-attachments/assets/df1511bf-6178-4c0c-8844-27eff5434178" />

So anything that should not be hardcoded should be templatized!!
<img width="1844" height="909" alt="image" src="https://github.com/user-attachments/assets/9508772e-e7e1-40c8-964a-395a9f9f6e26" />

<img width="1834" height="804" alt="image" src="https://github.com/user-attachments/assets/84abc0f6-5da1-4cd3-b464-d8a9d02ed8fc" />

That's how you define dictionary in the values.yaml file and use it in a template.

So basically we you install a helm chart, it uses files in the template directory and then combines it with the information about the releases like the release name or any other info, + the data stored in the values.yaml + the chart details to form the final version of the manifest files to deploy resources on K8s.
<img width="1852" height="815" alt="image" src="https://github.com/user-attachments/assets/9971ca2b-2371-4d0b-919f-f903c54a6459" />

Make sure the chart is working as intended.
<img width="519" height="894" alt="image" src="https://github.com/user-attachments/assets/07789f18-3b26-4c90-9a5b-697fd6f29d6c" />

lint - it basically checks the syntax errors and all.
template - it basically shows us what will be manifest generated after placing the values in the template locally.
<img width="1846" height="885" alt="image" src="https://github.com/user-attachments/assets/4092bf64-0281-4f20-8c26-c5575e59a516" />

There are other errors as well that these two commands can't catch like writing container instead of containers as it sees the templating and yaml format is correct, so what's wrong is the Kubernetes manifest format, so only K8s can tell us that this is wrong to catch this we have this dry-run command.

So in --dry-run basically it pretends to install that package, and give us the errors if any that K8s would be giving us in the real install.
<img width="1840" height="996" alt="image" src="https://github.com/user-attachments/assets/4b9f8e18-2218-45f9-a8d7-279cc6297f37" />

---

# Functions in Helm

<img width="1765" height="891" alt="image" src="https://github.com/user-attachments/assets/03b63d10-77a3-417c-badc-1dbb4b3c4fcf" />

Basically if we don't have values in the values.yaml, so it should have some default value to fall back on, that's where Functions comes...
so that i should not fail creating pods....

<img width="1784" height="876" alt="image" src="https://github.com/user-attachments/assets/d3e3eb28-b076-4498-93cf-f87b8bdd7fe2" />

So here basically "upper" is the function and ".Values.image.repository" is the argument.

There are many other kinds of functions as well! Refer Helm docs,
<img width="1407" height="944" alt="image" src="https://github.com/user-attachments/assets/89835ba5-dd01-42fb-8b2c-df61070e1ad7" />

<img width="1854" height="758" alt="image" src="https://github.com/user-attachments/assets/6f13ec16-9182-4b38-a117-525af5ae0675" />

---

# Pipelines

just as there are functions, but we most commonly use pipelines...basically using the pipe symbol, 
Example:
<img width="1797" height="182" alt="image" src="https://github.com/user-attachments/assets/045e1cd3-20da-4beb-a824-90592b4cce74" />

basically moving that function from front to the back with the pipe symbol.

---

# Conditionals

Now there might be a need if there's no related value present in the values.yaml so we don't want to have that in the template file, so that's where conditionals come, where basically you don't want to render those lines!!

here, conditionals are all part of the templating language so its in the curly braces, 
<img width="1838" height="776" alt="image" src="https://github.com/user-attachments/assets/b8b96c44-b9d2-4d3a-8d60-297b9e9f76c5" />
if value is set 

if not set
<img width="1803" height="787" alt="image" src="https://github.com/user-attachments/assets/815ac31c-4fe2-423c-b5a1-d62347124518" />

<img width="1321" height="819" alt="image" src="https://github.com/user-attachments/assets/728814dd-a6f5-41f9-bbc3-e22ddd291158" />
to trim the extra space/lines with use "-" just after the second curly brace.

Instead of operators, here we basically use functions for everything.
<img width="1717" height="982" alt="image" src="https://github.com/user-attachments/assets/8e3edbf6-d44d-45e7-a260-8d5b35b6288b" />

Common example of Conditionals is like whether you want to create that specific K8s object or not...
we can add conditional around the entire template file as well!!
<img width="1849" height="601" alt="image" src="https://github.com/user-attachments/assets/1d71fa43-b02c-40ce-b105-fdae3a605a63" />

---

# Scopes in Helm Charts (With)

The "." in the .Release.Name or whatever like the first "." represents the root scope.
<img width="1423" height="534" alt="image" src="https://github.com/user-attachments/assets/84054866-d5f9-4253-82bd-7fae6899ad2f" />
Its the root scope by default if you don't set it.

<img width="1662" height="863" alt="image" src="https://github.com/user-attachments/assets/643d5480-a2e7-423b-89b8-8cdd789f1be2" />
this is scope hierarchy...

For the root scope there "$" sign, generally used when you are in some different scope(within the with block) and you want to point to root.
<img width="1693" height="960" alt="image" src="https://github.com/user-attachments/assets/8dd54774-bbb3-4fa0-8adc-050961109c5c" />

---



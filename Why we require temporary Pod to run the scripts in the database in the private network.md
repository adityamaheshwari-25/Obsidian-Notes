The Kubernetes API can create and manage Kubernetes resources, but it can’t execute SQL on RDS by itself. RDS speaks the PostgreSQL protocol; it needs a client such as `psql` to connect and send the script.

Your command uses your local `kubectl` to ask the Kubernetes API to start a pod. That pod runs `psql` from inside the VPC and connects to RDS. You could run `psql` directly from your own machine instead, if your machine has network access to the RDS endpoint and PostgreSQL port 5432 is allowed.



and also we have done the same thing in the SwiftPay application, like created one VM to connect to that VNet and run those migration scripts in the MySQL database managed by Azure.
Its the same thing, just now in the K8s and AWS world with the Pods and VPC.

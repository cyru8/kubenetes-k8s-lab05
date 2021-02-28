# kubenetes-k8s-lab05
Create Ingress Routing

Kubernetes have advanced networking capabilities that allow Pods and Services to communicate inside the cluster's network. An Ingress enables inbound connections to the cluster, allowing external traffic to reach the correct Pod.

Ingress enables externally-reachable urls, load balance traffic, terminate SSL, offer name based virtual hosting for a Kubernetes cluster.

In this scenario you will learn how to deploy and configure Ingress rules to manage incoming HTTP requests.

Step 1 - Create Deployment

To start, deploy an example HTTP server that will be the target of our requests. The deployment contains three deployments, one called webapp1 and a second called webapp2, and a third called webapp3 with a service for each.

cat deployment.yaml
Task

Deploy the definitions with kubectl apply -f deployment.yaml

The status can be viewed with kubectl get deployment



Step 2 - Deploy Ingress

The YAML file ingress.yaml defines a Nginx-based Ingress controller together with a service making it available on Port 80 to external connections using ExternalIPs. If the Kubernetes cluster was running on a cloud provider then it would use a LoadBalancer service type.

The ServiceAccount defines the account with a set of permissions on how to access the cluster to access the defined Ingress Rules. The default server secret is a self-signed certificate for other Nginx example SSL connections and is required by the Nginx Default Example.

cat ingress.yaml
Task

The Ingress controllers are deployed in a familiar fashion to other Kubernetes objects with kubectl create -f ingress.yaml

The status can be identified using kubectl get deployment -n nginx-ingress

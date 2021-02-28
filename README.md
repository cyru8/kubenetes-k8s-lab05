# kubenetes-k8s-lab05
<<<<<<< HEAD
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
=======
>>>>>>> 48ff2e6b2dd710e8fe4b662de0cc2f2bc000e9e2


Step 2 - Deploy Ingress

The YAML file ingress.yaml defines a Nginx-based Ingress controller together with a service making it available on Port 80 to external connections using ExternalIPs. If the Kubernetes cluster was running on a cloud provider then it would use a LoadBalancer service type.

The ServiceAccount defines the account with a set of permissions on how to access the cluster to access the defined Ingress Rules. The default server secret is a self-signed certificate for other Nginx example SSL connections and is required by the Nginx Default Example.

cat ingress.yaml
Task

The Ingress controllers are deployed in a familiar fashion to other Kubernetes objects with kubectl create -f ingress.yaml

The status can be identified using kubectl get deployment -n nginx-ingress


######


Step 3 - Deploy Ingress Rules

Ingress rules are an object type with Kubernetes. The rules can be based on a request host (domain), or the path of the request, or a combination of both.

An example set of rules are defined within cat ingress-rules.yaml

The important parts of the rules are defined below.

The rules apply to requests for the host my.kubernetes.example. Two rules are defined based on the path request with a single catch all definition. Requests to the path /webapp1 are forwarded onto the service webapp1-svc. Likewise, the requests to /webapp2 are forwarded to webapp2-svc. If no rules apply, webapp3-svc will be used.

This demonstrates how an application's URL structure can behave independently about how the applications are deployed.

- host: my.kubernetes.example
  http:
    paths:
    - path: /webapp1
      backend:
        serviceName: webapp1-svc
        servicePort: 80
    - path: /webapp2
      backend:
        serviceName: webapp2-svc
        servicePort: 80
    - backend:
        serviceName: webapp3-svc
        servicePort: 80

Task

As with all Kubernetes objects, they can be deployed via kubectl create -f ingress-rules.yaml

Once deployed, the status of all the Ingress rules can be discovered via kubectl get ing

######

Step 4 - Test


With the Ingress rules applied, the traffic will be routed to the defined place.

The first request will be processed by the webapp1 deployment.

curl -H "Host: my.kubernetes.example" 172.17.0.38/webapp1

The second request will be processed by the webapp2 deployment.

curl -H "Host: my.kubernetes.example" 172.17.0.38/webapp2

Finally, all other requests will be processed by webapp3 deployment.

curl -H "Host: my.kubernetes.example" 172.17.0.38

######


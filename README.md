# SteerD Presto Kubernetes Operator

[Kubernetes](https://kubernetes.io/docs/home/) is an open source container orchestration engine for automating deployment, scaling, and management of containerized applications. [Operators](https://kubernetes.io/docs/concepts/extend-kubernetes/operator/) are software extensions to Kubernetes that make use of custom resources to manage applications and their components. Operators follow Kubernetes principles, notably the control loop.

SteerD Presto Operator is a Kubernetes Operator for Presto to manage Presto clusters which are deployed as custom resources. In short, the task of configuring, creating, managing, automatically scaling up and scaling-in of Presto cluster(s) in a Kubernetes environment has been made simple, easy and quick.

## Deploying Operator

### Deploying Operator

*Step 1:* Enable metrics server, if not already enabled. [See this](https://github.com/kubernetes-sigs/metrics-server). This is needed for horizontal pod autoscaling.

*Step 2:* Deploy the CRD
```bash
$ kubectl apply -f deploy/crds/falarica.io_prestos_crd.yaml
```
*Step 3:* Create a new namespace for the Steerd Presto Operator
```bash
$ kubectl create ns steerd-presto-operator
```  
*Step 4:* modify the namespace where you will install the Steerd Presto Operator
```bash
$ sed -i 's/namespace: .*/namespace: steerd-presto-operator/' deploy/operator.yaml
```
*Step 5:* Launch the operator
```bash
$ kubectl apply -f deploy/operator.yaml
```  
 
## Deploy Presto Cluster

Deploy the presto cluster
```bash
$ ## Deploy Presto
$ kubectl apply -f deploy/crds/falarica_prestodb.yaml  
```

## Further Details 

- [Creating Presto Cluster](docs/prestoresource.md)
- [Managing Presto Cluster](docs/status.md)
- [Autoscaling](docs/autoscaling.md)
- [Catalogs](docs/catalog.md)
- [Services](docs/service.md)
- [Additional Volumes](docs/additionalvolumes.md)
- [HTTPS Support](docs/https.md)
- [Caveats/Future Work](docs/caveats.md)

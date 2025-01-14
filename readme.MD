# K8S concepts

* namespace

```
kubectl apply -f 01-namespace.yaml
kubectl get namespaces
kubectl delete -f 01-namespace.yaml
```

* pod: smallest deployable unit in k8s. it can contain one or more containers

When multiple containers run in the same pod in Kubernetes, they share certain resources and can communicate with each other using localhost. This is useful for tightly coupled applications that need to share resources such as storage or network.

* Shared Network: Containers in the same pod share the same network namespace, meaning they can communicate with each other using localhost and share the same IP address.
* Shared Storage: Containers in the same pod can share storage volumes, allowing them to read and write to the same files.
* Shared Lifecycle: Containers in the same pod are managed as a single unit and share the same lifecycle. If one container in the pod fails, the entire pod is restarted.

Logging and Monitoring:

Use Case: Collecting logs from the main application container and sending them to a centralized logging system.
Example: A pod with an application container running a web server and a sidecar container running a log collector like Fluentd.


Proxying and Service Mesh:

Use Case: Managing network traffic, such as load balancing, service discovery, and security policies.
Example: A pod with an application container and a sidecar container running an Envoy proxy as part of a service mesh like Istio.
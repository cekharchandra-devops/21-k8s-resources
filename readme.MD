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


# Annotations

Annotations in Kubernetes are key-value pairs that can be attached to objects such as pods, services, and deployments. They are used to store arbitrary metadata that can be utilized by tools, libraries, and other systems. Unlike labels, annotations are not used to identify or select objects but can provide additional context or information about the object.

Real-Time Scenarios Where Annotations Are Useful

**Monitoring and Logging:**

Scenario: You want to integrate your Kubernetes pods with a monitoring system like Prometheus. Annotations can be used to specify which metrics should be collected and how they should be scraped.
Example: Adding Prometheus scrape annotations to a pod.

```
apiVersion: v1
kind: Pod
metadata:
  name: monitored-pod
  annotations:
    prometheus.io/scrape: "true"
    prometheus.io/path: "/metrics"
    prometheus.io/port: "8080"
spec:
  containers:
    - name: app-container
      image: myapp:latest
      ports:
        - containerPort: 8080
```

**Ingress Configuration:**

Scenario: You want to configure specific settings for an Ingress resource, such as enabling SSL redirection or setting custom timeouts.
Example: Adding annotations to an Ingress resource for SSL redirection.

```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: example-ingress
  annotations:
    nginx.ingress.kubernetes.io/ssl-redirect: "true"
    nginx.ingress.kubernetes.io/proxy-read-timeout: "60"
spec:
  rules:
    - host: example.com
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: example-service
                port:
                  number: 80
```

**Deployment Metadata:**

Scenario: You want to store metadata about the deployment, such as the Git commit hash or build number, to track which version of the code is running.
Example: Adding build metadata annotations to a deployment.

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: example-deployment
  annotations:
    build.commit: "abc123"
    build.number: "42"
....

```

**Custom Metrics and Autoscaling:**

Scenario: You want to use custom metrics for autoscaling your application. Annotations can be used to specify the custom metrics to be collected.
Example: Adding custom metrics annotations to a pod for autoscaling

```
apiVersion: v1
kind: Pod
metadata:
  name: custom-metrics-pod
  annotations:
    custom.metrics.k8s.io/requests-per-second: "true"
spec:
  containers:
    - name: app-container
      image: myapp:latest
``
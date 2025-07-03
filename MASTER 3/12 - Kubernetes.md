
## 1. Background: The Problem Before Kubernetes

### Challenges Before Kubernetes

- **Siloed teams and processes**:
    - Developers (Dev) focused on delivering features quickly.
    - Operations (Ops) focused on system uptime, stability, and security.
    - Lack of standardized environments between Dev and Ops caused **"it works on my machine"** issues.
        
- **Complex application delivery**:
    - Deployments were often manual, error-prone, and environment-specific.
    - Scaling up or down required physical or virtual server reconfigurations.
    - Rollbacks and updates had no consistent strategy.
        
- **Limited automation**:
    - Automation scripts were often brittle and tailored to specific systems.
    - Monitoring, healing, and load balancing had to be set up manually or via third-party tools.
    - High availability and fault tolerance required significant custom engineering effort.

### Rise of Containerization (e.g., Docker)

- Containers made it possible to:
    - **Package applications with all their dependencies**.
    - **Run consistently** across different environments (dev, test, prod).
    - Isolate processes without the overhead of virtual machines.
        
- However, containers alone did not solve:
    - **Scheduling** (what runs where and when?).
    - **Load balancing** (how to distribute traffic across containers?).
    - **Resiliency** (what happens when a container crashes?).
    - **Security and networking** between services.

### Need for Orchestration

To fully leverage containers in production, teams needed orchestration platforms to:
- **Schedule and distribute containers** across clusters of machines.
- **Monitor container health** and restart failed containers automatically.
- **Scale workloads up/down** based on demand.
- **Deploy updates with minimal downtime**, including rollbacks if something breaks    
- **Manage service discovery and networking**, so services can find and talk to each other.
- **Centralize configuration and secrets management** securely

---

### Kubernetes

Kubernetes emerged from these needs as:

- A **portable**, **extensible**, **open-source** platform for managing containerized workloads.
    
- A system built around the principle of **declarative infrastructure** ("define the desired state and let the system maintain it").
    
- A comprehensive solution that brought together scheduling, scaling, healing, updating, and service management under one unified control plane.

- An orchestration tool designed not only to run containers, but to support **cloud-native application patterns** like microservices, autoscaling, and infrastructure as code.

---

## 3. CNCF Ecosystem Tools

The CNCF hosts a broad range of tools and projects that complement Kubernetes:

- **Kubernetes**: The core orchestrator for managing containerized applications.
    
- **OpenTelemetry**: A standard framework for collecting distributed traces, logs, and metrics across systems.
    
- **ArgoCD**: A GitOps-based continuous deployment tool that integrates closely with Kubernetes.
    
- **Helm**: A package manager for Kubernetes applications using templated YAML configurations.
    
- **Prometheus** and **Grafana**: For monitoring and visualization.
    

These tools help complete the ecosystem needed for production-grade, cloud-native deployments.

---

## 4. Kubernetes Architecture

### Control Plane

The **control plane** manages the overall state of the Kubernetes cluster. It makes global decisions (e.g., scheduling) and detects/responds to cluster events.

- **kube-apiserver**: The front-end of the Kubernetes control plane. All operations (from `kubectl`, other services, or components) go through the API server.
    
- **etcd**: A distributed key-value store used to persist cluster state, such as resource definitions and configuration.
    
- **controller-manager**: Continuously reconciles the actual state of the cluster to the desired state (e.g., creating pods, handling failures).
    
- **scheduler**: Determines which worker node a new pod should be placed on, based on resource availability and scheduling policies.
    

### Worker Nodes

Worker nodes are machines (physical or virtual) that run the application workloads.

- **kubelet**: A node agent that receives Pod specifications from the API server and ensures the containers are running as expected.
    
- **Container Runtime**: Software responsible for starting and running containers (e.g., containerd, CRI-O, or Docker in legacy setups).
    
- **kube-proxy**: Manages networking rules to route traffic to the appropriate Pods on a node.
    

Both the control plane and worker nodes can be scaled and replicated for high availability and fault tolerance.

---

## 6. Core Kubernetes Resources

In Kubernetes, everything is treated as a **resource**. These resources are defined declaratively (typically in YAML files) and applied using the Kubernetes API (commonly via `kubectl`). The control plane then ensures the actual cluster state matches the desired configuration.

### Pod

A **Pod** is the smallest deployable unit in Kubernetes. It typically encapsulates a **single container**, but may include multiple containers that need to share resources such as storage or networking.

#### Use Cases
- Running a single microservice.
- Using the **sidecar pattern** (e.g., logging agent or proxy container alongside main app).

#### Characteristics
- Ephemeral (deleted and recreated, not updated in-place).
- Not resilient: if a Pod dies, it doesn’t automatically restart unless managed by higher-level objects like a ReplicaSet.

#### Example YAML

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-app
spec:
  containers:
    - name: my-container
      image: nginx:1.21
      ports:
        - containerPort: 80
```

#### Common Commands

```bash
kubectl apply -f pod.yaml       # Create the pod
kubectl get pods                # List running pods
kubectl describe pod my-app     # Inspect pod details
kubectl logs my-app             # View logs from the container
kubectl delete pod my-app       # Delete the pod
```

### ReplicaSet

A **ReplicaSet** ensures a specified number of identical Pods are running at all times.

#### Use Cases
- Ensuring availability and basic fault tolerance for a Pod.

#### Characteristics
- Automatically replaces failed or deleted Pods.
- Rarely used directly; usually managed through a Deployment.

#### Example YAML

```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: my-app-rs
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
        - name: my-container
          image: nginx:1.21
          ports:
            - containerPort: 80
```

#### Common Commands

```bash
kubectl apply -f replicaset.yaml      # Create the ReplicaSet
kubectl get rs                        # List ReplicaSets
kubectl scale rs my-app-rs --replicas=5  # Change replica count
kubectl delete rs my-app-rs           # Delete the ReplicaSet
```

---

### Deployment

A **Deployment** is the most commonly used controller in Kubernetes. It manages ReplicaSets, enabling declarative updates, rollbacks, and autoscaling.

#### Use Cases
- Managing stateless applications.
- Enabling rolling updates without downtime.
- Scaling services up or down.

#### Characteristics
- Automatically creates and manages underlying ReplicaSets.
- Can pause/resume rollout, rollback to previous versions, and track deployment status.

#### Example YAML

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 1
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
        - name: my-container
          image: nginx:1.21
          ports:
            - containerPort: 80
```

#### Common Commands

```bash
kubectl apply -f deployment.yaml                # Create the deployment
kubectl get deployments                         # List deployments
kubectl rollout status deployment/my-app-deployment  # Check rollout status
kubectl rollout undo deployment/my-app-deployment    # Rollback to previous version
kubectl scale deployment my-app-deployment --replicas=5  # Scale manually
kubectl delete deployment my-app-deployment     # Delete the deployment
```

---

### Namespace

**Namespaces** logically divide cluster resources and isolate groups of resources.

#### Use Cases
- Environment separation (dev, staging, prod).
- Resource quota management and access control.
- Multi-tenancy support.

#### Characteristics
- Default namespaces include:
  - `default`: default workspace for all resources.
  - `kube-system`: components managed by Kubernetes (like CoreDNS, kube-proxy).
  - `kube-public`: publicly accessible resources (e.g., cluster info).
- You can create custom namespaces for projects or teams.

#### Example YAML

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: dev-environment
```

#### Common Commands

```bash
kubectl create namespace dev-environment         # Create a new namespace
kubectl get namespaces                           # List all namespaces
kubectl delete namespace dev-environment         # Delete a namespace
kubectl get pods -n kube-system                  # List system pods in kube-system
kubectl config set-context --current --namespace=dev-environment  # Set default namespace for current context
```

---

### How They Work Together

- A **Deployment** creates a **ReplicaSet**.
- The **ReplicaSet** manages multiple identical **Pods**.
- All these resources can be scoped to a specific **Namespace**.
- Resource definitions are applied declaratively using `kubectl` or GitOps tools like ArgoCD or Flux.


---

## 8. Networking and Access

In Kubernetes, networking is a critical aspect that enables communication between Pods, between services, and from external clients to the cluster. Kubernetes provides abstractions to make this communication reliable and manageable.

### Service

A **Service** is a stable abstraction over a dynamic set of Pods. Pods can die and get recreated with new IPs, but a Service gives clients a consistent way to communicate with them.

#### Key Features

- **Pod discovery via label selectors**: Services select target Pods using label matching.
    
- **Stable DNS name and virtual IP**: Services get a DNS name (`service.namespace.svc.cluster.local`) and a virtual IP to route traffic.
    
- **Load balancing**: Distributes traffic across matching Pods.
    
- **Service types**:
    - `ClusterIP` (default): Accessible only within the cluster.
    - `NodePort`: Exposes the service on a static port across all nodes.
    - `LoadBalancer`: Integrates with cloud provider to provision an external load balancer.

#### Example YAML (ClusterIP)

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-app-service
spec:
  selector:
    app: my-app
  ports:
    - port: 80
      targetPort: 8080
      protocol: TCP
  type: ClusterIP
```

#### Example YAML (NodePort)

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-app-nodeport
spec:
  selector:
    app: my-app
  ports:
    - port: 80
      targetPort: 8080
      nodePort: 30036
  type: NodePort
```

#### Common Commands

```bash
kubectl apply -f service.yaml                    # Create service
kubectl get services                             # List all services
kubectl describe service my-app-service          # Inspect service config
kubectl delete service my-app-service            # Delete service
```

### Ingress

An **Ingress** is a powerful Kubernetes resource for managing external access to services over HTTP and HTTPS. It allows routing based on domain names and URL paths.

#### Key Features

- **Layer 7 (HTTP) routing**:
    
    - Route requests to different services based on host (e.g., `api.example.com`) or path (e.g., `/login`, `/admin`).
        
- **TLS termination**: Handle HTTPS by terminating SSL with secrets storing certificates.
    
- **Single entry point**: Acts as a unified reverse proxy for multiple services.
    

#### Ingress Controller Requirement

Ingress resources do nothing on their own—they require an **Ingress Controller** to implement the rules (e.g., `nginx-ingress`, `traefik`, `HAProxy`, or cloud-managed controllers like AWS ALB Ingress).

#### Example YAML

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: my-app-ingress
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
    - host: myapp.example.com
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: my-app-service
                port:
                  number: 80
```

#### With TLS (HTTPS)

```yaml
spec:
  tls:
    - hosts:
        - myapp.example.com
      secretName: myapp-tls-secret
  rules:
    - host: myapp.example.com
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: my-app-service
                port:
                  number: 80
```

#### Common Commands

```bash
kubectl apply -f ingress.yaml                    # Create ingress
kubectl get ingress                              # List ingress resources
kubectl describe ingress my-app-ingress          # Inspect ingress details
kubectl delete ingress my-app-ingress            # Delete ingress
```


### Internal DNS

- Kubernetes runs a DNS service (typically **CoreDNS**) to resolve service names within the cluster.
    
- Each service gets an internal DNS name in the format:
    
    ```
    <service-name>.<namespace>.svc.cluster.local
    ```
    
- This allows Pods and services to discover each other using service names instead of IP addresses.
    

### Real-world Example: Web Application Stack

Let’s say you have a frontend, a backend API, and a database. You might expose them like this:

- **Services**:
    - `frontend-service`: NodePort or LoadBalancer
    - `api-service`: ClusterIP
    - `db-service`: ClusterIP

- **Ingress**:
    - Route `example.com` → `frontend-service`
    - Route `example.com/api` → `api-service`
        
- **TLS**:
    - Secure the entire domain with HTTPS using a TLS secret and certificate.


---

## 10. Configuration and Secrets

In Kubernetes, it's essential to keep your application configurations **decoupled from the container images**. This allows you to reuse the same image across environments (development, staging, production) by injecting different configurations as needed. Kubernetes provides two primary mechanisms to achieve this:

- `ConfigMap` for non-sensitive configuration.
- `Secret` for sensitive data (like credentials or API keys).

### ConfigMap

A **ConfigMap** is used to store **non-sensitive** configuration data as key-value pairs. These values can be injected into Pods in various ways, such as environment variables, command-line arguments, or mounted files.

#### Use Cases

- Defining app environment variables.
- Providing configuration files (like JSON, YAML, INI).
- Parameterizing application behavior without modifying code.

#### Example YAML

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
data:
  APP_MODE: "production"
  APP_COLOR: "blue"
  CONFIG_JSON: |
    {
      "featureEnabled": true,
      "logLevel": "debug"
    }
```

#### Using ConfigMap in a Pod (as env vars)
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: configmap-demo
spec:
  containers:
    - name: demo-container
      image: nginx
      env:
        - name: MODE
          valueFrom:
            configMapKeyRef:
              name: app-config
              key: APP_MODE
        - name: COLOR
          valueFrom:
            configMapKeyRef:
              name: app-config
              key: APP_COLOR
```

#### Mounting as Files
```yaml
      volumeMounts:
        - name: config-volume
          mountPath: /etc/config
  volumes:
    - name: config-volume
      configMap:
        name: app-config
```

#### Common Commands
```bash
kubectl create configmap app-config --from-literal=APP_MODE=production
kubectl apply -f configmap.yaml
kubectl get configmap app-config -o yaml
kubectl delete configmap app-config
```

### Secret

A **Secret** stores **sensitive information** such as database passwords, API tokens, SSH keys, TLS certificates, etc.

While Secrets are base64-encoded (not encrypted by default), they are treated differently from ConfigMaps in terms of access control and visibility. Kubernetes RBAC and service account policies should restrict access to them.

#### Use Cases

- Storing credentials, access tokens.
- TLS certificates for HTTPS endpoints.
- SSH keys or service passwords.

#### Example YAML (Generic Secret)
```yaml
apiVersion: v1
kind: Secret
metadata:
  name: app-secret
type: Opaque
data:
  DB_PASSWORD: c2VjdXJlcGFzc3dvcmQ=   # base64 of 'securepassword'
  API_KEY: MTIzNDU2Nzg5               # base64 of '123456789'
```

> To generate base64 values:  
> `echo -n "securepassword" | base64`

#### Using Secret in a Pod (as env vars)
```yaml
      env:
        - name: DB_PASSWORD
          valueFrom:
            secretKeyRef:
              name: app-secret
              key: DB_PASSWORD
```

#### Mounting as Files
```yaml
      volumeMounts:
        - name: secret-volume
          mountPath: /etc/secret
          readOnly: true
  volumes:
    - name: secret-volume
      secret:
        secretName: app-secret
```

#### Common Commands
```bash
kubectl create secret generic app-secret --from-literal=DB_PASSWORD=securepassword
kubectl apply -f secret.yaml
kubectl get secret app-secret -o yaml
kubectl delete secret app-secret
```

### Best Practices

- Keep secrets separate from application code and configuration.
- Limit access to secrets using **RBAC policies**.
- Use tools like **SealedSecrets** (Bitnami) or **HashiCorp Vault** for secret encryption and dynamic secret management.
- Avoid hardcoding configuration in Pod specs; externalize into ConfigMaps or Secrets.


---

## 7. Resource Management and Scheduling

Kubernetes allows fine-grained control over how much CPU and memory each container can use.

- **requests**: The amount of CPU/memory guaranteed to a container. Kubernetes uses this for scheduling.
    
- **limits**: The maximum amount a container can use. Exceeding this can cause throttling (for CPU) or termination (for memory).
    

If a container exceeds its **memory limit**, it is killed by the kernel’s Out Of Memory (OOM) killer.  
If it exceeds its **CPU limit**, it is throttled (slowed down), not killed.

> ⚠ For JVM-based applications, it is recommended to set the maximum heap size (`-Xmx`) equal to the memory **request**, not the limit, to avoid OOM kills.

#### Quality of Service (QoS) Classes

Kubernetes assigns each Pod a QoS class based on its resource configuration:

- **BestEffort**: No requests or limits set. Lowest priority.
    
- **Burstable**: Requests and limits are set but not equal. Medium priority.
    
- **Guaranteed**: Requests and limits are both set and equal. Highest priority.
    

This affects scheduling and eviction decisions under resource pressure.


---

## 14. Kubernetes in Cloud Network Architecture

Kubernetes is cloud-agnostic but deeply integrated with cloud providers when deployed in environments like AWS, Azure, or GCP. Understanding how cloud networking concepts map to Kubernetes behavior is critical for secure, reliable, and scalable deployments.

### DNS (Domain Name System)

DNS in Kubernetes provides **service discovery**—allowing applications to find and communicate with one another dynamically without hardcoding IP addresses.

#### How it works in Kubernetes:

- Kubernetes uses **CoreDNS** (formerly kube-dns) to resolve internal service names.
    
- Each Service in a cluster gets a DNS name like:
    
    ```
    my-service.my-namespace.svc.cluster.local
    ```
    
- When a Pod makes a request to `my-service`, CoreDNS resolves it to the correct ClusterIP or external IP based on service type.
    

#### Example:

```bash
curl http://my-api.my-namespace.svc.cluster.local
```


### Load Balancer

A **LoadBalancer** in Kubernetes is a type of Service that exposes an application to external traffic, typically through integration with the cloud provider’s native load balancer.

#### In AWS:
- Kubernetes creates an **Elastic Load Balancer (ELB)** automatically when you deploy a Service of type `LoadBalancer`.

#### In Kubernetes:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-app
spec:
  type: LoadBalancer
  selector:
    app: my-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 8080
```

> The cloud provider provisions an external IP or DNS name through its load balancer system (e.g., `abcdef123.elb.amazonaws.com`) and routes traffic into the cluster.

### VPC (Virtual Private Cloud)

A **VPC** is a logically isolated section of the cloud provider’s network. Kubernetes clusters typically run inside a VPC to:

- Isolate workloads from the internet and from other tenants.
- Control network flow using routing tables, security groups, and firewall rules.
- Enable private communication between services, nodes, and control planes.

#### Key Components inside a VPC:

- Subnets (public/private)
- NAT Gateways
- Internet Gateways
- Route Tables
- Security Groups (like firewalls)
- ENIs (Elastic Network Interfaces for Pods in AWS)

> All Kubernetes nodes (workers + control plane) are assigned IPs inside the VPC subnets.

### Public vs Private Subnets

Subnets within a VPC are categorized based on their ability to reach the internet:

#### Public Subnets

- Associated with an **Internet Gateway**.
- Resources (like EC2/Kubernetes nodes) in these subnets can **send and receive traffic from the internet**.
- Used for:
    - Bastion hosts
    - Load balancers
    - Ingress controllers

#### Private Subnets
- Do **not have direct internet access**.
- Resources can initiate outbound internet requests only if a **NAT Gateway** is configured.
- More secure for:
    - Kubernetes worker nodes
    - Control plane components (etcd, scheduler)
    - Internal services (databases, APIs)

> Best practice: **Run the Kubernetes control plane and nodes in private subnets**, and expose only ingress/load balancer interfaces to the public internet.

### Network Flow Overview

1. **External traffic (HTTP)** hits the **cloud load balancer** (via DNS).
2. It is routed into the **Ingress Controller** (e.g., NGINX) running in Kubernetes.
3. The Ingress routes the request to the right **Service**, which finds the right **Pod(s)**.
4. Internal Pod-to-Pod communication is handled over the **Pod network** (via CNI plugin).
5. Outbound traffic from Pods to the internet goes through:
    - Node’s IP (in AWS via NAT Gateway)
    - Or a **public IP** if the Pod/Node is in a public subnet.


![[Pasted image 20250702160700.png]]

    

---

## 11. Advanced Scheduling and Pod Placement

Kubernetes provides powerful mechanisms to influence where Pods are scheduled in a cluster. This is essential for improving performance, availability, fault tolerance, and resource isolation.

### nodeSelector

`nodeSelector` is the simplest way to constrain a Pod to run on nodes with specific labels.

#### Use Case

For example, run a Pod only in a particular Availability Zone (`eu-west-3a`) or on nodes with a GPU.

#### Example

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: zoned-pod
spec:
  nodeSelector:
    topology.kubernetes.io/zone: eu-west-3a
  containers:
    - name: app
      image: nginx
```

#### Limitations

- Only supports **exact match** on labels.
- No soft preferences or logical conditions.

### nodeAffinity

`nodeAffinity` offers a more flexible and expressive way to define where Pods should be scheduled.

#### Two Modes

- **`requiredDuringSchedulingIgnoredDuringExecution`**:  
    Hard rules that must be met for scheduling.
    
- **`preferredDuringSchedulingIgnoredDuringExecution`**:  
    Soft rules; the scheduler will try to honor them but may ignore them if not possible.

#### Example (Required)

```yaml
affinity:
  nodeAffinity:
    requiredDuringSchedulingIgnoredDuringExecution:
      nodeSelectorTerms:
        - matchExpressions:
            - key: topology.kubernetes.io/zone
              operator: In
              values:
                - eu-west-3a
```

#### Example (Preferred)

```yaml
affinity:
  nodeAffinity:
    preferredDuringSchedulingIgnoredDuringExecution:
      - weight: 1
        preference:
          matchExpressions:
            - key: disktype
              operator: In
              values:
                - ssd
```


---

### podAffinity and podAntiAffinity

These affinity rules operate on Pods rather than nodes.

#### Use Cases
- Co-locate related services (e.g., cache + API).
- Distribute replicas across failure domains to avoid single points of failure.
    

#### podAffinity Example
```yaml
affinity:
  podAffinity:
    requiredDuringSchedulingIgnoredDuringExecution:
      - labelSelector:
          matchLabels:
            app: my-app
        topologyKey: "kubernetes.io/hostname"
```

#### podAntiAffinity Example
```yaml
affinity:
  podAntiAffinity:
    preferredDuringSchedulingIgnoredDuringExecution:
      - weight: 100
        podAffinityTerm:
          labelSelector:
            matchLabels:
              app: my-app
          topologyKey: "kubernetes.io/hostname"
```

#### Notes

- `topologyKey` defines the granularity (e.g., node, zone).
- Anti-affinity is often used in high availability scenarios.

---

## 12. Taints and Tolerations

Kubernetes **taints** allow you to mark a node so that Pods **won’t be scheduled** there unless they have an appropriate **toleration**.

This is the reverse of affinity: instead of attracting Pods to nodes, it repels them.

### Taints

A taint has three parts:

```
<key>=<value>:<effect>
```

- **Effects**:
    - `NoSchedule`: Pod will not be scheduled unless it tolerates the taint.
    - `PreferNoSchedule`: Scheduler avoids placing a Pod but doesn’t guarantee it.
    - `NoExecute`: Existing Pods will be evicted unless tolerated.

#### Example

```bash
kubectl taint nodes node1 dedicated=infra:NoSchedule
```

---

### Tolerations
Pods can declare tolerations to bypass taints and be scheduled onto specific nodes.
#### Example

```yaml
tolerations:
  - key: "dedicated"
    operator: "Equal"
    value: "infra"
    effect: "NoSchedule"
```

### Common Use Cases

- Isolate **GPU workloads**, **critical services**, or **billing environments**.
    
- Prevent **non-critical workloads** from affecting performance of sensitive applications.
    

---

## 13. Network Policies

By default, all Pods in a Kubernetes cluster can talk to each other freely. **NetworkPolicies** provide a way to restrict traffic **at the IP and port level** inside the cluster.

### Capabilities

- Control **ingress** (incoming) and **egress** (outgoing) traffic at the Pod level.
    
- Define rules based on:
    - Pod selectors
    - Namespace selectors
    - IP blocks
    - Port numbers

### Example: Ingress Policy

Only allow traffic to a Pod from Pods with the label `role: frontend`.

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-frontend
spec:
  podSelector:
    matchLabels:
      app: my-api
  ingress:
    - from:
        - podSelector:
            matchLabels:
              role: frontend
```

### Example: Deny All

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: deny-all
spec:
  podSelector: {}
  policyTypes:
    - Ingress
```

> Note: An empty `podSelector` matches all Pods in the namespace.


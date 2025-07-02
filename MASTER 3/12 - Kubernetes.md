
- Before Kubernetes : Dev vs Ops / need of orchestration
- Creation of Kub, standard use everywhere
- CNCF
	- Kub
	- OpenTelemetry
	- ArgoCD
	- ...

## Architecture
- Control Pane
	- Controller Manager
	- Scheduler
	- Kube Api
	- etcd
- Worker node
	- kubelet
	- Container runtime (containerd, etc.)
- Control Pane and Worker Nodes are both replicated

---

**Kub => All is resource**

Pod:
- Wraps up to 2 containers (sidecar pattern)
- config in yml

ReplicaSet:
- INSTEAD OF PODS
- Important to use labels in the config
- Can create replicas of pods
- Auto healing
- Scaling / AutoScaling (HPA)
- High Availibility

Deployment:
- INSTEAD OF REPLICASET
- Handles ReplicaSets
- Rolling Update / Rollout
- Rollback

Namespace:
- default namespace
- To organize the projects

---

- Resources managements
	- Request guaranteed
	- Limit not guaranteed
- With java, we set the jvm XMX at the request usually
	- XMX <= request
- Best Effort vs Burstable vs Guaranteed
	- request < limit
	- request = limit

---

Service:
- can select a deployment label
- define input / target ports

- Internal DNS (core DNS) in K8s

Ingress

Certificate TLS


# Kubernetes Pods

#### 0. Pods

- [1. Questions for Pods](./0-Pods/01-Pod.md)

- [P.1 Simple Nginx Pod](./0-Pods/P.1-Simple-Nginx-Pod.md)
- [P.2 Multi-Container Pod](./0-Pods/P.2-Multi-container-pods.md)

---

## **1. Introduction to Pods**

### [1.1 What is a Pod?](./01-Intro-to-Pods/1.1-what-is-pod.md)

- Definition and purpose of Pods
- Difference between Pods and containers
- Single vs. Multi-container Pods

### [1.2 Pod Lifecycle](./01-Intro-to-Pods/1.2-Pod-Lifecycle.md)

- Phases of a Pod (Pending, Running, Succeeded, Failed, etc.)
- Pod termination and cleanup
- Pod states and status fields

### [1.3 Creating and Managing Pods](./01-Intro-to-Pods/1.3-Creating-Managing-Pods.md)

- Basic `kubectl` commands to create, view, and manage Pods
- YAML configuration for Pods
- Labels, selectors, and annotations

## **2. Pod Networking**

### [2.1 Pod-to-Pod Communication](./02-Pod-Networking/2.1-Pod-to-Pod-Communication.md)

- Understanding how Pods communicate within a cluster
- ClusterIP and networking models in Kubernetes
- DNS for Pods

### [2.2 Service Discovery](./02-Pod-Networking/2.2-Service-Discovery.md)

- How Pods are discovered and exposed
- Role of Services in Pod communication

### [2.3 Networking Policies](./02-Pod-Networking/2.3-Networking-Policies.md)

- Network isolation between Pods
- Creating and applying Network Policies

## **3. Pod Storage Management**

### [Topics to be covered](./03-Pod-Storage/Future-Topics.md)

### [3.1 Volume Types](./03-Pod-Storage/3.1-Volumes-in-Pods.md)

- Types of Volumes (emptyDir, hostPath, persistentVolume, etc.)

### [3.2 Persistent Volumes (PVs) and Persistent Volume Claims (PVCs)](./03-Pod-Storage/3.2-pv-pvc.md)

- **PV Lifecycle**: Creation, binding, reclaiming, and deletion.
- **PVC Binding**: How a PVC requests storage and gets bound to a PV.
- **Dynamic Provisioning**: Automatically creating PVs using StorageClasses when PVCs are requested.
- **Access Modes**: Understanding `ReadWriteOnce`, `ReadOnlyMany`, and `ReadWriteMany`.

## **4. Pod Scheduling**

### [4.1 Pod Affinity and Anti-affinity](./04-Pod-Scheduling/4.1-Pod-Affinity-Anti-affinity.md)

- Scheduling Pods based on affinity rules
- Soft and hard affinity/anti-affinity

### [4.2 Node Selectors and Taints](./04-Pod-Scheduling/4.2-Node-Selectors-Taints.md)

- Assigning Pods to specific nodes
- Taints and tolerations for advanced scheduling

### [4.3 Resource Requests and Limits](./04-Pod-Scheduling/4.3-Resource-Requests-Limits.md)

- Setting CPU and memory requests/limits for Pods
- Handling resource overcommitment and QoS (Quality of Service) classes

## **5. Pod Monitoring and Logging**

### [5.1 Monitoring Pod Health](./05-Pod-Monitoring-Logging/5.1-Monitoring-Pod-Health.md)

- Readiness and Liveness Probes
- Pod health checks

### [5.2 Pod Logging](./05-Pod-Monitoring-Logging/5.2-Pod-Logging.md)

- Accessing and managing logs from Pods
- Sidecar containers for logging

## **6. Pod Scaling and Autoscaling**

### [6.1 Manual Scaling](./06-Pod-Scaling-and-Autoscaling/6.1-Manual-Scaling.md)

- Scaling Pods manually using `kubectl`
- Replication Controllers and ReplicaSets

### 6.2 [Horizontal Pod Autoscaler (HPA)](./06-Pod-Scaling-and-Autoscaling/6.2-HPA.md)

- Setting up HPA for automatic scaling
- Metrics used for scaling (CPU, memory, custom metrics)

## **7. Advanced Pod Patterns**

### [7.1 Init Containers](./07-Advanced-Pod-Patterns/7.1-Init-Containers.md)

- Role and use cases of Init Containers
- Configuring Init Containers in Pods

### [7.2 Sidecar Containers](./07-Advanced-Pod-Patterns/7.2-Sidecar-Containers.md)

- Understanding Sidecar pattern
- Implementing Sidecars for logging, monitoring, and proxies

### [7.3 Ephemeral Containers](./07-Advanced-Pod-Patterns/7.3-Ephemeral-Containers.md)

- Debugging with Ephemeral Containers
- Use cases and configuration

## **8. Pod Disruption Budget (PDB)**

### [8.1. Purpose of PDBs](./08-Pod-Disruption-Budget/8.1-Purpose-of-PDBs.md)

- Ensuring minimum Pod availability during disruptions.
- Preventing full application downtime.

### [8.2. PDB Configuration](./08-Pod-Disruption-Budget/8.2-PDB-Configuration.md)

- Setting `minAvailable` or `maxUnavailable` Pods.
- Using labels to apply PDBs to specific Pods.

### [8.3. Use Cases](./08-Pod-Disruption-Budget/8.3-Use-Cases.md)

- Maintaining service uptime during node maintenance or updates.
- Balancing Pod availability and cluster operations.

---

## **8. Pod Security**

### 8.1 Security Contexts

- Configuring security contexts for Pods and containers
- Setting user permissions and capabilities

### 8.2 Pod Security Policies

- Implementing Pod Security Admission (PSA)
- Restricting Pod creation based on security contexts

### 8.3 Securing Pod Communication

- TLS encryption between Pods
- Role-based access control (RBAC) for Pods

## **9. Troubleshooting Pods**

### **9.1 Common Issues**

- Troubleshooting Pod startup failures
- Dealing with OOM (Out of Memory) and CPU throttling

### **9.2 Debugging Techniques**

- Using `kubectl describe` and `kubectl logs` for debugging
- Attaching to Pods and inspecting containers

### **9.3 CrashLoopBackOff and Pending Pods**

- Diagnosing and resolving CrashLoopBackOff issues
- Analyzing Pending Pods and resolving scheduling issues

---
